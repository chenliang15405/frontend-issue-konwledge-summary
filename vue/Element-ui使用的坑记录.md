### Element-ui使用的坑记录

1. 不同浏览器的dateTimePicker选择问题

   > 在苹果的ios浏览器 safari、IE这些浏览器中，日期格式为yyyy/mm/dd，中间是/来分隔，chrome中都可以显示

   在使用dateTimePicker中，需要在页面中显示为yyyy-mm-dd这种格式，代码如下：

   ```html
   <el-date-picker
        @change="dateChange"
        v-model="ruleForm.endTime"
        type="datetime"
        placeholder="选择日期时间"
        value-format=" yyyy-MM-dd HH:mm:ss"
        format="yyyy-MM-dd HH:mm:ss"
        >
   </el-date-picker>
   
   // js
   
   dateChange(val) {
   	this.ruleForm.endTime = val;
   }
   ```

   因为是通过@change中的方法，来进行给ruleForm.endTime赋值，并不是直接赋值，因为直接通过数据绑定获取的时间格式有问题：自动会在后面加上时区，不太方便处理，所以直接通过这种change方法获取的数据，是经过value-format来格式化的数据，直接赋值，就会按照yyyy-MM-dd hh:mm:ss来进行设置。

   在safari和IE中选择是之后，页面无法显示，因为这两个浏览器，默认显示的日期格式为: yyyy/mm/dd

   解决方式：

    先将yyyy-MM-dd 转换为 yyyy/MM/dd，再提交的时候，再将yyyy/MM/dd转换为yyyy-MM-dd即可

   ```js
   dateChange(val) {
     val = val.replace(/-/g, '/');
     this.ruleForm.endTime = val;
   }
   
   submitForm (formName) {
   	this.ruleForm.endTime = this.ruleForm.endTime.replace(/\//g, '-');
     // 提交表单
     ...
   }
   ```

