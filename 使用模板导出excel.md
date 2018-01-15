### 1.引入jar包坐标

```java
<dependency>
    <groupId>net.sf.jxls</groupId> 
    <artifactId>jxls-core</artifactId> 
    <version>1.0.6</version> 
</dependency>
```

### 2.添加excel模板

### 3.代码编写

```java
try {
  	//根据模板创建工作薄
	HSSFWorkbook workbook = new HSSFWorkbook(new ClassPathResource("export_orders.xls").getInputStream());
  	//创建数据模型
  	Map<String, Object> dataModel = new HashMap<>();
	//绑定数据：o是excel模板中遍历的属性名称，order为查询出的数据集合
	dataModel.put("o", order);
  	
	XLSTransformer transformer = new XLSTransformer();
  	//填充数据
	transformer.transformWorkbook(workbook, dataMap);
  	//将生成的文件写出
	workbook.write(os);
} catch (IOException e) {
	e.printStackTrace();
}finally{
	if(null != workbook){
		try {
			workbook.close();
		} catch (IOException e) {
          	e.printStackTrace();
		}
	}
}
```



