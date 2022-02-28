<template>
    <!-- <a-table
      :columns="columns" 
      :data-source="tabData" 
      :row-key="(record) => record.key"
      :customRow="tableClick"
      expandRowByClick
      :row-selection="{selectedRowKeys: selectedRowKeys, onSelectAll: onSelectAll, onSelect: onSelect}" 
    /> -->
    <a-table
        :columns="columns"
        :row-key="row => row.key"
        :data-source="tabData"
        :customRow="rowClick"
        :row-selection="{selectedRowKeys: selectedRowKeys, onSelectAll: onSelectAll, onSelect: onSelect}"
    >
        <template slot="name" slot-scope="text">
            <span>
                {{text}}
            </span>
        </template>
    </a-table>
        <!-- :row-selection="rowSelection"
        :expanded-row-keys.sync="expandedRowKeys" -->
</template>

<script>
const columns = [
    {
        title: "文件名称",
        dataIndex: "name",
        key: "name",
        scopedSlots: { customRender: "name" }
    },
    {
        title: "类型",
        dataIndex: "type",
        key: "type",
        width: "12%",
    },
    {
        title: "文件大小",
        dataIndex: "size",
        width: "12%",
        key: "size",
    },
    {
        title: "修改时间",
        dataIndex: "updataTime",
        width: "12%",
        key: "updataTime",
    },
    {
        title: "上传人员",
        dataIndex: "uploadName",
        width: "12%",
        key: "uploadName",
    },
];

const data = [
    {
        key: 1,
        name: "文件夹名称",
        type: '文件夹',
        size: "-",
        updataTime: "09-22 12:00",
        uploadName: "赵小刚",
        children: [
            {
                key: 2,
                name: "文件夹名称",
                type: '文件夹',
                size: "-",
                updataTime: "09-22 12:00",
                uploadName: "赵小刚",
                children:[
                    {
                        key: 3,
                        name: "文件名称",
                        type: 'PDF文件',
                        size: "100kb",
                        updataTime: "09-22 12:00",
                        uploadName: "赵小刚",
                    },
                    {
                        key: 4,
                        name: "文件名称",
                        type: 'PDF文件',
                        size: "100kb",
                        updataTime: "09-22 12:00",
                        uploadName: "赵小刚",
                    },
                    {
                        key: 5,
                        name: "文件名称",
                        type: 'PDF文件',
                        size: "100kb",
                        updataTime: "09-22 12:00",
                        uploadName: "赵小刚",
                    }
                ]
            },
        ],
    },
    // {
    //     key: '2',
    //     name: "Joe Black",
    //     age: 32,
    //     address: "Sidney No. 1 Lake Park",
    // },
];
// const rowSelection = {
//     onChange: (selectedRowKeys, selectedRows) => {
//         console.log(
//             `selectedRowKeys: ${selectedRowKeys}`,
//             "selectedRows: ",
//             selectedRows
//         );
//     },
//     onSelect: (record, selected, selectedRows) => {
//         console.log(record, selected, selectedRows);
//     },
//     onSelectAll: (selected, selectedRows, changeRows) => {
//         console.log(selected, selectedRows, changeRows);
//     },
// };
export default {
    name: "TableSel",
    props: {
        // bordered: Boolean,
        // loading: [Boolean, Object],
        // columns: Array,
        // dataSource: Array,
        // rowKey: {
        //     type: [String, Function],
        //     default: "key",
        // },
        // pagination: {
        //     type: [Object, Boolean],
        //     default: true,
        // },
        // selectedRows: Array,
        // expandedRowKeys: Array,
        // expandedRowRender: Function,
    },
    data() {
        return {
            selectedRowKeys: [],
            columns,
            tabData:data,
            // columns: [
            //     {
            //         title: "Name",
            //         dataIndex: "name",
            //         key: "name",
            //     },
            //     {
            //         title: "Age",
            //         dataIndex: "age",
            //         key: "age",
            //         width: "12%",
            //     },
            //     {
            //         title: "Address",
            //         dataIndex: "address",
            //         width: "30%",
            //         key: "address",
            //     },
            // ],

            // tabData: [
            //     {
            //         key: 1,
            //         name: "John Brown sr.",
            //         age: 60,
            //         address: "New York No. 1 Lake Park",
            //         children: [
            //             {
            //                 key: 11,
            //                 name: "John Brown",
            //                 age: 42,
            //                 address: "New York No. 2 Lake Park",
            //             },
            //             {
            //                 key: 12,
            //                 name: "John Brown jr.",
            //                 age: 30,
            //                 address: "New York No. 3 Lake Park",
            //                 children: [
            //                     {
            //                         key: 121,
            //                         name: "Jimmy Brown",
            //                         age: 16,
            //                         address: "New York No. 3 Lake Park",
            //                     },
            //                 ],
            //             },
            //             {
            //                 key: 13,
            //                 name: "Jim Green sr.",
            //                 age: 72,
            //                 address: "London No. 1 Lake Park",
            //                 children: [
            //                     {
            //                         key: 131,
            //                         name: "Jim Green",
            //                         age: 42,
            //                         address: "London No. 2 Lake Park",
            //                         children: [
            //                             {
            //                                 key: 1311,
            //                                 name: "Jim Green jr.",
            //                                 age: 25,
            //                                 address: "London No. 3 Lake Park",
            //                             },
            //                             {
            //                                 key: 1312,
            //                                 name: "Jimmy Green sr.",
            //                                 age: 18,
            //                                 address: "London No. 4 Lake Park",
            //                             },
            //                         ],
            //                     },
            //                 ],
            //             },
            //         ],
            //     },
            //     {
            //         key: 2,
            //         name: "Joe Black",
            //         age: 32,
            //         address: "Sidney No. 1 Lake Park",
            //     },
            // ],
            // rowSelection,
            expandRowByClick: false,
            expandedRowKeys: ['1'],
        };
    },
    methods: {
        onSelectAll(selected) {
            if (selected) {
                const tabData = this.tabData;
                const arr = [];
                setVal(tabData, arr);
                this.selectedRowKeys = arr;
            } else {
                this.selectedRowKeys = [];
            }
            function setVal(list, arr) {
                list.forEach(v => {
                  arr.push(v.key);
                  if (v.children) {
                    setVal(v.children, arr);
                  }
                });
            }
        },
        onSelect(record, selected) {
            const set = new Set(this.selectedRowKeys);
            // const tabData = this.tabData;
            const key = record.key;
            console.log(record,selected)
            if (selected) {
                set.add(key);
                record.children && setChildCheck(record.children);
                // setParentCheck(key);
            } else {
                set.delete(key);
                record.children && setChildUncheck(record.children);
                // setParentUncheck(key);
            }
            this.selectedRowKeys = Array.from(set);
            // 设置父级选择
            // function setParentCheck(key) {
            //     let parent = getParent(key);
            //     if (parent) {
            //       set.add(parent.key);
            //       setParentCheck(parent.key);
            //     }
            // }
            // 设置父级取消，如果父级的子集有选择，则不取消
            // function setParentUncheck(key) {
            //     let childHasCheck = false,
            //     parent = getParent(key);
            //     if (parent) {
            //         let childlist = parent.children;
            //         childlist.forEach(function(v) {
            //             if (set.has(v.key)) {
            //                 childHasCheck = true;
            //             }
            //         });
            //         if (!childHasCheck) {
            //             set.delete(parent.key);
            //             setParentUncheck(parent.key);
            //         }
            //     }
            // }
            // // 获取当前对象的父级
            // function getParent(key) {
            //     for (let i = 0; i < tabData.length; i++) {
            //         if (tabData[i].key === key) {
            //             return null;
            //         }
            //     }
            //     return _getParent(tabData);
            //     function _getParent(list) {
            //         let childlist,
            //         isExist = false;
            //         for (let i = 0; i < list.length; i++) {
            //             if ((childlist = list[i].children)) {
            //                 childlist.forEach(function(v) {
            //                     if (v.key === key) {
            //                         isExist = true;
            //                     }
            //                 });
            //                 if (isExist) {
            //                     return list[i];
            //                 }
            //                 if (_getParent(childlist)) {
            //                     return _getParent(childlist);
            //                 }
            //             }
            //         }
            //     }
            // }
            // // 设置child全选
            function setChildCheck(list) {
                list.forEach(function(v) {
                    set.add(v.key);
                    v.children && setChildCheck(v.children);
                });
            }
            // // 设置child取消
            function setChildUncheck(list) {
                list.forEach(function(v) {
                    set.delete(v.key);
                    v.children && setChildUncheck(v.children);
                });
            }
        },
        /** 点击a-table中的行后，展开或关闭其子行 */
        // tableClick(record, index){
        //     return {
        //         style:{
        //             cursor:'pointer',
        //         },
        //         on: {
        //             click: () => {
        //                 // console.log(record,index);
        //                 this.expandRowByClick = !this.expandRowByClick;
        //             }
        //         }
        //   	}
        // },
        rowClick(record, index) {
            return {
                on:{
                    click:(event) => {
                        console.log(record, index, event, "5555");
                    },
                    mouseenter:(event) => {
                        console.log(record, index, event, "666");
                    },
                    mouseleave:(event) => {
                        console.log(record, index, event, "888");
                    },
                }
                // onClick: (event) => {
                //     console.log(record, index, event, "5555");
                // },
                // onMouseenter: (event) => {
                //     console.log(record, index, event, "666");
                // },
                // onMouseleave: (event) => {
                //     console.log(record, index, event, "888");
                // },
            };
        }
    },
};
</script>

<style scoped lang="less">
</style>