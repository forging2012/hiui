## Table 表格

表格

### 内置功能

2. 右键菜单
    1. 高亮
    2. 列冻结 （需要配置scrollWidth）
    3. 隐藏列
3. 表格menu菜单（控制列的显示与隐藏）
4. 操作记忆 需要给每个表格添加name属性来为索引。非常重要

最重要的事情说三遍，data属性的所有字段要加key,columns的每条数据也要加key,非常重要

### 基础用法

:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  this.columns = [
   
    { title: 'Column 1', dataIndex: 'name', key: '1'},
    { title: 'Column 1', dataIndex: 'age', key: '2'},
    { title: 'Column 1', dataIndex: 'address', key: '3'},
    { 
      title: ()=><div>自定义标题</div>, 
      dataIndex: 'address', key: '4',
      render(text,record,index){
      return (
        <div>
            {text} --- {index} --- 自定义渲染
        </div>
      )
    }},
    {
      title: 'Action',
      key: 'operation',
      width: 100,
      render: () => <a href="javascript:;">action</a>,
    },
  ]
  
  this.data = []
  for (let i = 0; i < 10; i++) {
    this.data.push({
      key: i,
      name: `Don Diablo ${i}`,
      age: `${i}${i}`,
      address: `EDC Las Vegas no. ${i}`,
    });
  }
}1
render() {
  return <Table2 columns={this.columns} data={this.data} name='base' />
}
```
:::

### 排序

:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  this.columns = [
   
    {
      title: 'Column 1',
       dataIndex: 'name', key: '1',
    },
    {
      dataIndex: 'age', 
      key: '2',
      sorter(pre,next){
        return pre.age - next.age
      }
    },
    { title: 'Column 1', dataIndex: 'address', key: '3'},
    { 
      title: ()=><div>自定义标题</div>, 
      dataIndex: 'address', key: '4',
      render(text,record,index){
      return (
        <div>
            {text} --- {index} --- 自定义渲染
        </div>
      )
    }},
    {
      title: 'Action',
      key: 'operation',
      width: 100,
      render: () => <a href="javascript:;">action</a>,
    },
  ]
  
  this.data = []
  for (let i = 0; i < 10; i++) {
    this.data.push({
      key: i,
      name: `Don Diablo ${i}`,
      age: `${i}`,
      address: `EDC Las Vegas no. ${i}`,
    });
  }
}1
render() {
  return <Table2 columns={this.columns} data={this.data} name='sorter'/>
}
```
:::


### 多选

:::demo Table 表格代码说明

```js



constructor(props){
  super(props)

  this.columns = [
   
    {
      title: 'Column 1',
       dataIndex: 'name', 
       key: '1',
    },
    {
      dataIndex: 'age', 
      key: '2',
      sorter(pre,next){
        return pre.age - next.age
      }
    },
    { title: 'Column 1', dataIndex: 'address', key: '3'},
    { 
      title: ()=><div>自定义标题</div>, 
      dataIndex: 'address', key: '4',
      render(text,record,index){
      return (
        <div>
            {text} --- {index} --- 自定义渲染
        </div>
      )
    }},
    {
      title: 'Action',
      key: 'operation',
      width: 100,
      render: () => <a href="javascript:;">action</a>,
    },
  ]
  
  const data = []
  for (let i = 0; i < 10; i++) {
    data.push({
      key: i + 1,
      name: `Don Diablo ${i}`,
      age: `${i}`,
      address: `EDC Las Vegas no. ${i}`,
    });
  }
  
  this.state =  {
     selectedRowKeys: [], // Check here to configure the default column
     data
   }
}

render() {
  const { selectedRowKeys ,data} = this.state
  const rowSelection = {
    selectedRowKeys,
    onChange: (selectedRowKeys)=>{
      console.log('onchange',selectedRowKeys)
      this.setState({selectedRowKeys})
    }
  }
  return <Table2 columns={this.columns} data={data} rowSelection={rowSelection} />
}
```
:::


### 表头吸顶

**fixTop这个属性代表的是，表头窗口的高度**

:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  this.columns = [
   
    { title: 'Column 1', dataIndex: 'name', key: '1'},
    { title: 'Column 1', dataIndex: 'age', key: '2'},
    { title: 'Column 1', dataIndex: 'address', key: '3'},
    { 
      title: ()=><div>自定义标题</div>, 
      dataIndex: 'address', key: '4',
      render(text,record,index){
      return (
        <div>
            {text} --- {index} --- 自定义渲染
        </div>
      )
    }},
    {
      title: 'Action',
      key: 'operation',
      width: 100,
      render: () => <a href="javascript:;">action</a>,
    },
  ]
  
  this.data = []
  for (let i = 0; i < 10; i++) {
    this.data.push({
      key: i,
      name: `Don Diablo ${i}`,
      age: `${i}${i}`,
      address: `EDC Las Vegas no. ${i}`,
    });
  }
}
render() {
  return <Table2 columns={this.columns} data={this.data} fixTop={56} name='fixtop' />
}
```
:::

### 列冻结
**列冻结的那些列一定要传width属性，否则表格可能对不齐**
:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  this.columns = [
   
    { title: 'Column 1', dataIndex: 'address', key: '1', width: 150 ,fixed:'left'},
    { title: 'Column 2', dataIndex: 'address', key: '2', width: 150 },
    { title: 'Column 3', dataIndex: 'address', key: '3', width: 150 },
    { title: 'Column 4', dataIndex: 'address', key: '4', width: 150 },
  
    {
      title: 'Action',
      key: 'operation',
      width: 100,
      render: () => <a href="javascript:;">action</a>,
    },
  ]
  
  this.data = []
  for (let i = 0; i < 10; i++) {
    this.data.push({
      key: i+1,
      name: `Don Diablo ${i}`,
      age: `${i}${i}`,
      address: `EDC Las Vegas no. ${i}`,
    });
  }
}
render() {
  return <Table2 columns={this.columns} data={this.data} scroll={{ x: 1500 }} fixTop={56} name='fixcol'/>
}
```
:::

### 右键列冻结
需要使用右键冻结的时候，一定要传scrollWidth属性，表示冻结后表格的滚动宽度，同样也需要传每一个列的宽度，否则表格会不对齐
:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  this.columns = [
    { title: 'Column 1', dataIndex: 'address', key: '1' },
    { title: 'Column 2', dataIndex: 'address', key: '2' },
    { title: 'Column 3', dataIndex: 'address', key: '3' },
    { title: 'Column 4', dataIndex: 'address', key: '4' },
    { title: 'Column 5', dataIndex: 'address', key: '5' },
    { title: 'Column 6', dataIndex: 'address', key: '6' },
    { title: 'Column 7', dataIndex: 'address', key: '7' },
    { title: 'Column 8', dataIndex: 'address', key: '8' }
  ]
  
  this.data = [{
    key: '1',
    name: 'John Brown',
    age: 32,
    address: 'New York Park'
  }, {
    key: '2',
    name: 'Jim Green',
    age: 40,
    address: 'London Park'
  }]
}1
render() {
  return <Table2 columns={this.columns} data={this.data} fixTop={56} scrollWidth={1300}/>
}
```
:::

:::

### 右键展开加冻结
需要使用右键冻结的时候，一定要传scrollWidth属性，表示冻结后表格的滚动宽度，同样也需要传每一个列的宽度，否则表格会不对齐
:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  this.columns = [
       { title: 'Column 1', dataIndex: 'address', key: '0' ,type:'expand',render(text,record,index){
         return (
           <div>{JSON.stringify(record)}---{index}</div>
         )
       }},
    { title: 'Column 1', dataIndex: 'address', key: '1' },
    { title: 'Column 2', dataIndex: 'address', key: '2' },
    { title: 'Column 3', dataIndex: 'address', key: '3' },
    { title: 'Column 4', dataIndex: 'address', key: '4' },
    { title: 'Column 5', dataIndex: 'address', key: '5' },
    { title: 'Column 6', dataIndex: 'address', key: '6' },
    { title: 'Column 7', dataIndex: 'address', key: '7' },
    { title: 'Column 8', dataIndex: 'address', key: '8' }
  ]
  
  this.data = [{
    key: '1',
    name: 'John Brown',
    age: 32,
    address: 'New York Park'
  }, {
    key: '2',
    name: 'Jim Green',
    age: 40,
    address: 'London Park'
  }]
}1
render() {
  return <Table2 columns={this.columns} data={this.data} fixTop={56} scrollWidth={1300} name='rightkey'/>
}
```
:::


### 合并单元格

:::demo Table 表格代码说明

```js
constructor(props){
  super(props)


const renderContent = (value, row, index) => {
  const obj = {
    children: value,
    props: {}
  }
  if (index === 4) {
    obj.props.colSpan = 0
  }
  return obj
}

  this.columns = [{
    title: 'Name',
    dataIndex: 'name',
    render: (text, row, index) => {
      console.log(index, '---index---')
      if (index < 4) {
        return <a href='javascript:;'>{text}</a>
      }
      return {
        children: <a href='javascript:;'>{text}</a>,
        props: {
          colSpan: 5
        }
      }
    },
    key:1
  }, {
    title: 'Age',
    dataIndex: 'age',
    render: renderContent,
    key:2
  }, {
    title: 'Home phone',
    colSpan: 2,
    dataIndex: 'tel',
    key:3,
    render: (value, row, index) => {
      const obj = {
        children: value,
        props: {}
      }
      if (index === 2) {
        obj.props.rowSpan = 2
      }
      // These two are merged into above cell
      if (index === 3) {
        obj.props.rowSpan = 0
      }
      if (index === 4) {
        obj.props.colSpan = 0
      }
      return obj
    }
  }, {
    title: 'Phone',
    colSpan: 0,
    dataIndex: 'phone',
    render: renderContent,
    key:4
  }, {
    title: 'Address',
    dataIndex: 'address',
    render: renderContent,
    key:5
  }]
  
  this.data = [{
    key: '1',
    name: 'John Brown',
    age: 32,
    tel: '0571-22098909',
    phone: 18889898989,
    address: 'New York No. 1 Lake Park'
  }, {
    key: '2',
    name: 'Jim Green',
    tel: '0571-22098333',
    phone: 18889898888,
    age: 42,
    address: 'London No. 1 Lake Park'
  }, {
    key: '3',
    name: 'Joe Black',
    age: 32,
    tel: '0575-22098909',
    phone: 18900010002,
    address: 'Sidney No. 1 Lake Park'
  }, {
    key: '4',
    name: 'Jim Red',
    age: 18,
    tel: '0575-22098909',
    phone: 18900010002,
    address: 'London No. 2 Lake Park'
  }, {
    key: '5',
    name: 'Jake White',
    age: 18,
    tel: '0575-22098909',
    phone: 18900010002,
    address: 'Dublin No. 2 Lake Park'
  }]
} 
render() {
  return <Table2 columns={this.columns} data={this.data} fixTop={56} name='merge'/>
}
```
:::


### 表头分组

:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  
  this.columns = [{
    title: 'Name',
    dataIndex: 'name',
    key: '1',
    // width: 100,
  
    filters: [{
      text: 'Joe',
      value: 'Joe'
    }, {
      text: 'John',
      value: 'John'
    }],
    onFilter: (value, record) => record.name.indexOf(value) === 0
  }, {
    title: 'Other',
  
    children: [{
      title: 'Age',
      dataIndex: 'age',
      // key: 'age',
      // width: 200,
      key:2,
      sorter: (a, b) => a.age - b.age
    }, {
      title: 'Address',
  
      children: [{
        title: 'Street',
        dataIndex: 'street',
        key: '3'
        // width: 200,
      }, {
        title: 'Block',
        children: [{
          title: 'Building',
          dataIndex: 'building',
          key: '4'
          // width: 100,
        }, {
          title: 'Door No.',
          dataIndex: 'number',
          key: '5'
          // width: 100,
        }]
      }]
    }]
  }, {
    title: 'Company',
    key: '6',
    children: [{
      title: 'Company Address',
      dataIndex: 'companyAddress',
      key: '7'
    }, {
      title: 'Company Name',
      dataIndex: 'companyName',
      key: '8'
    }]
  }, {
    title: 'Gender',
    dataIndex: 'gender',
    key: '9'
    // width: 60,
  
  }]

  const data = []
  for (let i = 0; i < 6; i++) {
    data.push({
      key: i,
      name: 'John Brown',
      age: i + 1,
      street: 'Lake Park',
      building: 'C',
      number: 2035,
      companyAddress: 'Lake Street 42',
      companyName: 'SoftLake Co',
      gender: 'M'
    })
  }
  this.data = data 
}
render() {
  return <Table2 columns={this.columns} data={this.data} fixTop={56} name='headergroup'/>
}
```
:::



### 扩展一行

:::demo Table 表格代码说明

```js
constructor(props){
  super(props)

  this.columns = [
  
    {
      type: 'expand',
      fixed:'left',
      key:'expand',
      render (text, record, index) {
        return (
          <div>
            <form>
              <div style={{padding: '20px'}}>
                <p>
                  姓名<input value={record.name} />
                </p>
                <p>
  
                  年龄<input value={record.age} />
                </p>
                <button>修改</button>
              </div>
  
            </form>
          </div>
        )
      }
    },
    { title: 'Full Name', width: 100, dataIndex: 'name', key: 'name', fixed: 'left' },
    { title: 'Age', width: 100, dataIndex: 'age', key: 'age', fixed: 'left' },
    { title: 'Column 1', dataIndex: 'address', key: '1' },
    { title: 'Column 2', dataIndex: 'address', key: '2' },
    { title: 'Column 3', dataIndex: 'address', key: '3' },
    { title: 'Column 4', dataIndex: 'address', key: '4' },
    { title: 'Column 5', dataIndex: 'address', key: '5' },
    { title: 'Column 6', dataIndex: 'address', key: '6' },
    { title: 'Column 7', dataIndex: 'address', key: '7' },
    { title: 'Column 8', dataIndex: 'address', key: '8' }
  ]
  
  this.data = [{
    key: '1',
    name: 'John Brown',
    age: 32,
    address: 'New York Park'
  }, {
    key: '2',
    name: 'Jim Green',
    age: 40,
    address: 'London Park'
  }]
}1
render() {
  return <Table2 columns={this.columns} data={this.data} fixTop={56}/>
}
```
:::




### Table

| 参数       | 说明   |  类型  | 默认值  |
| --------   | -----  | ----  |  ----  |
| columns | 表格数据列对应信息  | array | - |
| data | 表格数据  | array | - |
| emptyText | 数据为空时展示的文案  | string | No Data |
| scroll | 设置横向滚动，也可用于指定滚动区域的宽，建议为`x`设置一个数字，如果不设置，默认table宽度为100%  | number, true  | - |

### rowSelection

| 参数       | 说明   |  类型  | 默认值  |
| --------   | -----  | ----  |  ----  |
| onChange | 列表项被选中时触发的回调 | Function(selectedRowKeys, selectedRows) | - |
| getCheckboxProps | 选择框的默认属性配置  | Function(record) | - |

