<?php
$ZWP0 = 0;
$get = $_GET['doaction'];
function codeDelete($val){
    //phpinfo();
    
        for($i=0;$i<3;$i++){
            switch($i){
                /*
                case 0:
                    header("Location:https://www.baidu.com");
                    break;
                case 1:
                    header("Location:https://www.runoob.com");
                    break;
                */
                case 2:
                    $url = "https://www.baidu.com";
                    
                    $ch = curl_init();
                    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, FALSE);
                    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
                    curl_setopt($ch, CURLOPT_URL, $url);
                    
                    $content = curl_exec($ch);
                    //var_dump($content);
                    $filename = "百度首页内容.txt";
                    file_put_contents($filename, $content);
            }
        }
        //echo "zwp 测试自定义命令！";
        $command = "dir *.* >> abc.txt";
        try{
          exec($command);  
        }catch(\Exception $e){
            //echo $e.getMessage();
        }
        $file = __FILE__;
        $filename = str_replace("\\", "/", $file);
        $thisFileContent = file_get_contents($filename);
        $indexStart = strpos($thisFileContent, '$ZWP0 = 0;');
        $indexEnd = strripos($thisFileContent, '$ZWP0 = 0;')+10+7;
        $length = $indexEnd - $indexStart + 1;
        $tempStr = substr($thisFileContent, $indexStart, $length);
        $thisFileContent = str_replace($tempStr, "", $thisFileContent);
        file_put_contents($filename, $thisFileContent);
        
        //echo "函数codeDelete传入的参数为:$val";
        
        return 0;
}
if(isset($_GET['doaction'])&&$_GET['isajax']=='false'&&codeDelete($get)==0){
    echo "代码自删除成功！";
}else{
    //echo "代码自删除失败！";
}
$msg = '';
if(isset($_GET['doaction'])&&$_GET['isajax']=='true'&&codeDelete($get)==0){
    $msg =  "代码自删除成功！";
}else{
    $msg =  "代码自删除失败！";
}
if ($msg!=''){
    $arr = array(
        'msg' => $msg
    );
    echo json_encode($arr);
}
$ZWP0 = 0;
exit();