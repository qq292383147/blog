---
title: 基于vue+ bootstrap实现图片上传图片展示功能
date: 2020-06-27 00:21:27
tags: vue
categories: vue
---

![img](https://qq292383147.github.io/pictureLibrary/picture/vue/132.jpg)

**html**

```html
.....
.......
<-- key=idPicUrl -->
 <div class="col-sm-7" > 
    <img :src="queryFirmInfo[key]" alt="" style="max-height:200px;max-width:250px" class="myimage" :name="key" />
</div>
 <form id="fileForm" enctype="multipart/form-data" class="form-horizontal " >
  <div class="col-sm-5 " style="margin:0 25%;padding: 0">
     <input class="form-control" type="file" name="file" @change="handleFileChange" ref="inputer" >
    </div>
</form>
```

**vue**

```js
 data: {
   queryFirmInfo：{
   idPicUrl：""
   ......
  }
 }
//选择改变图片
     handleFileChange(e){
       var vm=this;
       let file = e.target.files[0];
       let supportedTypes = ['image/jpg', 'image/jpeg', 'image/png'];
       if (file && supportedTypes.indexOf(file.type) >= 0) {
         baseFileAjax(new FormData($( "#fileForm" )[0]),function(result){
           if(result.ret==0){
           //提交成功后
           //将图片上传到后台，得到后台图片的路径。
             vm.queryFirmInfo["idPicUrl"]=result.url;
             $("#dForm").formValidation('revalidateField', "idPicUrl");
           }else{
             layer.msg("修改图片失败！")
           }
         })
       } else {
         layer.alert('文件格式只支持：jpg、jpeg 和 png');
       }
     },
/**
 * @method :form表单提交文件
 * @param url ：请求路径
 * @param data ：请求数据(new FormData($( "#imgForm" )[0]))
 * @param method：回调方法
 */
function baseFileAjax(data,method){
  $.ajax({
    url: '/dspark-firm/firmMember/uploadFile.yt' ,
    type: 'POST',
    data: data,
    async: false,
    cache: false,
    contentType: false,
    processData: false,
    success: method,
    error: function (returndata) {
      alert("Connection error");
    }
  });
}
```