<template>
    <div class="PB-list" :style="{ zIndex: z }">
        <MdSlot ref="mdSlot" :title="'实体统一编辑'" @closeFun="closeFun">
            <template>
                <div>
                    <el-table 
                      :data=pagedEntities style="width: 100%;"
                    >
                        <el-table-column label="ID" prop="uid" width="70rem" align="center">
                        </el-table-column>
                        <el-table-column label="名称" align="center" width="180rem" class="name">
                            <template v-slot="scope">
                                <el-input v-model="scope.row.name"></el-input>
                            </template>
                        </el-table-column>
                        <el-table-column label="经度" align="center" width="110rem">
                            <template v-slot="scope">
                                <el-input-number v-model="scope.row.lon" :step="0.1" :min="-180"
                                    :max="180" controls-position="right" class="no-controls lonlat-input"></el-input-number>
                            </template>
                        </el-table-column>
                        <el-table-column label="纬度" align="center" width="110rem">
                            <template v-slot="scope">
                                <el-input-number v-model="scope.row.lat" :step="0.1" :min="-90"
                                    :max="90" controls-position="right" class="no-controls lonlat-input"></el-input-number>
                            </template>
                        </el-table-column>
                        
                        <el-table-column label="高度" align="center" width="110rem">
                            <template v-slot="scope">
                                <el-input-number v-model="scope.row.alt" :step="1"
                                 controls-position="right" class="no-controls height-input"></el-input-number>
                            </template>
                        </el-table-column>
                        
                        <el-table-column label="朝向" align="center" width="90rem">
                            <template v-slot="scope">
                                <el-input-number v-model="scope.row.heading" :step="1" :min="0" :max="360"
                                 controls-position="right" class="no-controls heading-input"></el-input-number>
                            </template>
                        </el-table-column>
                        <el-table-column label="操作" align="center" width="80rem">
                            <template v-slot="scope">
                                <el-button size="mini" type="primary" @click="reset(scope.$index)">
                                    重置
                                </el-button>
                            </template>
                        </el-table-column>
                    </el-table>
                    <el-pagination
                        style="margin-top: 16px; text-align: center;"
                        background
                        layout="pre, pager, next"
                        :current-page="currentPage"
                        :page-size="pageSize"
                        :total="entities.length"
                        @current-change="onCurrentPageChange">
                     </el-pagination>   
                </div>
            </template>
        </MdSlot>
    </div>
</template>
  
<script>

import MdSlot from "@/slots/MdSlot.vue";
import { Mdx_EventManager } from "^/Mdx_EventManager";
import { Mdx_DataManager } from "^/Mdx_DataManager";


export default {
    name: "editSelectedEntities",
    components: {
        MdSlot,
    },
    props: {
        data: {
            type: Object,
        },
        z: {
            type: String
        }
    },

    data() {
        return {
            defaultEntities: [],
            entities: [],
            currentPage: 1,
            pageSize: 5
        };
    },
    computed: {
        pagedEntities() {
            const start = (this.currentPage - 1) * this.pageSize;
            return this.entities.slice(start, start + this.pageSize);
        }
    },

    methods: {
        closeFun() {
            FeSubPub.publish(Mdx_EventManager.MDX_EVENTS.MDXE_UI_PB);
        },
        reset(index) {
            this.$set(this.entities, index, Mdx_DataManager.deepCopy(this.defaultEntities[index]));
        },
        onCurrentPageChange(page) {
            this.currentPage = page;
        }
    },
    created() {

    },
    mounted() {
        // console.log("editSelectedEntities mounted");
        // console.log(this.data);
        // this.defaultEntities = [];
        // for (let selectedId of this.data?.selectedIds) {
        //     let entityData = Mdx_DataManager.inst.dsSceneData.currentScenario.getMapEntitiesId(selectedId);
        //     if (!entityData) {
        //         continue;
        //     }
        //     let obj = {
        //         uid: entityData.uid,
        //         name: entityData.name,
        //         lon: entityData.position[0],
        //         lat: entityData.position[1],
        //         alt: entityData.position[2],
        //         heading: entityData.rotation[0],
        //     }
        //     this.defaultEntities.push(obj);
        // }
        this.defaultEntities = [
    {
        "uid": 10001,
        "name": "XXX指挥所(红)",
        "lon": 102.99731903485255,
        "lat": 43.09383378016085,
        "alt": 0,
        "heading": 0
    },
    {
        "uid": 10002,
        "name": "XXX指挥所(红)_1",
        "lon": 102.41823056300268,
        "lat": 36.53083109919571,
        "alt": 0,
        "heading": 0
    }
]
        this.entities = Mdx_DataManager.deepCopy(this.defaultEntities);
        console.log(this.entities)
    },

    destroyed() {
        console.log("editSelectedEntities destroyed");
    },
};
</script>

<style lang="scss" scoped>

::v-deep .no-controls {
    box-align: "center";
    .el-input-number__increase {
        width: getRem(10);
        display: none;
    }
    .el-input-number__decrease {
        width: getRem(10);
        display: none;
    }
    .el-input {
        
    }
    .el-input__inner {
        padding-left: getRem(10);
        padding-right: getRem(10);
    }
}

::v-deep .heading-input .el-input {
    width: getRem(80);
    text-align: center;
}

::v-deep .height-input .el-input {
    width: getRem(100);
    text-align: center;
}

::v-deep .lonlat-input .el-input {
    width: getRem(100);
    text-align: center;
}

::v-deep .el-table .el-table__cell {
    // 默认是12
    padding: getRem(5) 0;
}

.name {
    width: getRem(150);
    text-align: center;
}

::v-deep .el-table .cell  {
    // line-height: 13rem;
    // padding-left: 2rem;
    // padding-right: 2rem;
}

.PB-list {
    //   display: flex;
    width: getRem(780);
    height: getRem(600);
    position: fixed;
    top: 50%;
    left: 48%;
    transform: translate(-50%, -50%);
    z-index: 100;
    color: white;

    .pb-list-wrap {
        padding-bottom: getRem(20);
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        height: calc(100% - 20rem);

        .pb-table {
            width: 100%;
        }

        .pb-thead,
        .pb-tbody {
            .pb-row {
                font-size: getRem(16);
                height: getRem(28);
                line-height: getRem(20);
                margin: 0;
                padding: 0;

                .pb-name {
                    width: getRem(300);
                    text-align: center;
                }

                .pb-btn {
                    width: getRem(180);
                    color: skyblue;
                }
            }
        }

        .pb-thead {
            .pb-row {
                color: rgb(52, 204, 255);
                background-color: rgba(12, 113, 175, 50);
            }
        }

        .pb-tbody {
            .pb-row {
                background-color: rgba(12, 113, 175, 0.08);

                &:nth-child(2n + 1) {
                    background-color: rgba(11, 16, 33, 0.3);
                }

                .pb-btn {
                    cursor: pointer;
                }

                .pb-btn:hover {
                    color: rgb(14, 165, 225);
                }
            }
        }
    }
}

.pb-ind {
    width: getRem(70);
}

.reExperiment {
    text-align: left;
    font-size: getRem(14);
    cursor: pointer;
    color: skyblue;
    margin-bottom: getRem(10);
    text-decoration: underline;
}

.reExperiment:hover {
    color: rgb(14, 165, 225);
}
</style> 

  