<!doctype html>
<html lang="en">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no, minimal-ui" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<meta http-equiv="pragma" content="no-cache">
<meta http-equiv="cache-control" content="no-cache">
<meta http-equiv="expires" content="0" />
<title>单图上传</title>
<meta name="Keywords" content="">
<meta name="description" content="" />
<link rel="stylesheet" href="register.css">
<script type="text/javascript" src="jquery-1.8.3.min.js"></script>
<script type="text/javascript" src="uploadPreview.min.js"></script>
<script type="text/javascript">
window.onload = function () {	
	new uploadPreview({
	    UpBtn: "head",
	    DivShow: "doctorHeaddiv",
	    ImgShow: "doctorHeadShow",
	    Width:100
	});
	new uploadPreview({
		UpBtn: "card_pic",
		DivShow: "doctorIDdiv",
		ImgShow: "doctorIDShow",
		Width:100
	});

	new uploadPreview({
		UpBtn: "technical_pic",
		DivShow: "doctorZichengdiv",
		ImgShow: "doctorZichengShow",
		Width:100
	});
	new uploadPreview({
		UpBtn: "physiciancation_pic",
		DivShow: "doctorZhiyediv",
		ImgShow: "doctorZhiyeShow",
		Width:100
	});
}
</script>
</head>

<body>
	<form action="" enctype="multipart/form-data" method="post" id="from3">
		<div class="touxiangdiv">
			<div class="wrapdiv">
				<div class="doc_pic" id="doctorHeaddiv"><img id="doctorHeadShow" src="camera.png" width="100" height="100" style="border-radius:100px;"></div>
				<input type="file" class="input_file" id="head" name="head">
			</div>
			<p>建议上传白底，本人穿白大褂证件照</p>
		</div>

		<div class="main_pic">
			<div class="single_pic">
				<dl><dt>身份证<b>（必填）</b></dt><dd>请上传身份证正面照，个人信息必须清楚</dd></dl>
				<div class="jia">
					<div id="doctorIDdiv"><img id="doctorIDShow" src="jia.png" width="70" height="48"></div>
					<input type="file" class="input_filepic" id="card_pic" name="card_pic">
				</div>
			</div>
			<div class="single_pic">
				<dl><dt>医生职业注册证-盖章页<b>（必填）</b></dt><dd>清晰包括头像、编码、注册地点以及卫生厅盖章的彩色内页照！</dd></dl>
				<div class="jia">
					<div id="doctorZhiyediv"><img id="doctorZhiyeShow" src="jia.png" width="70" height="48"></div>
					<input type="file" class="input_filepic" id="physiciancation_pic" name="physiciancation_pic">
				</div>
			</div>
			<div class="single_pic">
				<dl><dt>医生职称证<b>（选填）</b></dt><dd>请上传带头像的职称证内页彩色照照片</dd></dl>
				<div class="jia">
					<div id="doctorZichengdiv"><img id="doctorZichengShow" src="jia.png" width="70" height="48"></div>
					<input type="file" class="input_filepic" id="technical_pic" name="technical_pic">
				</div>
			</div>
		</div>
		
		<div class="nbtn" style="margin-bottom:10px;padding-bottom:10px;">
			<p>您的资料不会被公开，仅使用问大夫医生认证审核</p>
			<input type="hidden" name="userid" value="{$_GET['userid']}" id="userid"/>
			<input type="submit" value="提交认证" class="next" id="submit" rel="0">
		</div>
	</form>

<script>
$(function(){
//参数设置
var mark 							= new Array();
var arr 							= new Array();
	
	arr['head'] 					    = new Array();
	arr['head']['reg'] 			        = '';
	arr['head']['null'] 			    = '请上传医生头像！';
		
	arr['card_pic'] 				    = new Array();
	arr['card_pic']['reg'] 		        = '';
	arr['card_pic']['null'] 		    = '请上传本人身份证！';
		
	arr['physiciancation_pic'] 			= new Array();
	arr['physiciancation_pic']['reg'] 	= '';
	arr['physiciancation_pic']['null'] 	= '请上传医生职业注册证-盖章页！';
		
	arr['technical_pic'] 			= new Array();
	arr['technical_pic']['reg'] 	= '';
	arr['technical_pic']['null'] 	= '请上传医生职称证！';

	//提交注册
	$('#from3').submit(function(){
		var rel = $('#submit').attr('rel');
		if(rel == 1){ //提交开关判断 0开1关
			return false;
		}
		check('physiciancation_pic');
		check('technical_pic');
		check('card_pic');
		check('head');
		if(mark['head'] && mark['card_pic'] && mark['physiciancation_pic']){
			$('#submit').attr('rel', '1').val('提交中...');
		} else {
			return false;
		}
	});

	//检测
	function check(name){
		mark[name] 	= false; //验证标识
		var str 	= $('#'+name).val();
		var reg 	= arr[name]['reg'];
			
		if (str == '') { //为空
			alert(arr[name]['null']);return false;
             layer.msg(arr[name]['null'], 1, 5);
        } else if (reg != '' && !reg.test(str)) { //规则错误
            alert(arr[name]['null']);return false;
        } else {
			mark[name] = true;
		}
		return false;
	}
});
</script>
</body>
</html>
