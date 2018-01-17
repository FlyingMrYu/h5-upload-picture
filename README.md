# h5-upload-picture
## h5 多图上传
# 多图文件上传
* html 
  >  <div id="fileList" class="flex flex-box flex-row flex-start flex-wrap">
   			<div id="addimg" class="flex flex-column flex-centerss addimg-div">
   			<img src="../image/add.png" style="width: 22px;height: 22px;padding-top: 7px;margin-bottom: 5px;">
   			<span class="addimg-title">添加照片</span>
  			</div>
  		</div>
   		<input type="file" id="fileElem" data-validate="fileElem" data-describedby="fileElem-description" multiple accept="image/*" onchange="handleFiles(this)" style="display: none">
 *  js
>    function handleFiles(obj) {
	  			var files = obj.files,
	   				img = new Image();
	  			//blob格式
	 			if(window.URL) {
	  				img.src = window.URL.createObjectURL(files[0]);
	   				img.width = 60;
	  				img.height = 60;
	  				img.onload = function(e) {
	  					window.URL.revokeObjectURL(this.src);
	 				}
	 				fileList.insertBefore(img, addimg);
          
         					//url blob转base64
   					var reader = new FileReader();
	 				reader.onload = function() {
				img.src = reader.result;
			 		}
					if(files[0]) {
	 				reader.readAsDataURL(files[0]);
	  		
					img.width = 60;
			 		img.height = 60;
	 				img.onload = function(e) {
					}
					fileList.insertBefore(img, addimg);
				} else if(window.FileReader) {
					//base64
					var reader = new FileReader();
					reader.readAsDataURL(files[0]);
					reader.onload = function(e) {
						console.log(files[0].name + "," + e.total + " bytes");
						img.src = this.result;
						img.width = 60;
						img.height = 60;
						fileList.insertBefore(img, addimg);
					}
				} else {
					//ie
					obj.select();
					obj.blur();
					var nfile = document.selection.createRange().text;
					document.selection.empty();
					img.src = nfile;
					img.onload = function() {
						console.log(nfile + "," + img.fileSize + " bytes");
					}
					fileList.insertBefore(img, addimg);
				}
			}
			
			

