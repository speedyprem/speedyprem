<?php
if (isset($_POST['submit'])) {

	$alpha = "abcdefghijklmnopqrstuvwxyz";
$alpha_upper = strtoupper($alpha);
$numeric = "0123456789";
$special = ".-+=_,!@$#*%<>[]{}215435435@#$%^&*";
$chars = "";
 
if (isset($_POST['length'])){
    // if you want a form like above
    if (isset($_POST['alpha']) && $_POST['alpha'] == 'on')
        $chars .= $alpha;
     
    if (isset($_POST['alpha_upper']) && $_POST['alpha_upper'] == 'on')
        $chars .= $alpha_upper;
     
    if (isset($_POST['numeric']) && $_POST['numeric'] == 'on')
        $chars .= $numeric;
     
    if (isset($_POST['special']) && $_POST['special'] == 'on')
        $chars .= $special;
     
    $length = $_POST['length'];
}else{
    // default [a-zA-Z0-9]{9}
    $chars = $alpha . $alpha_upper . $numeric;
    $length = $_POST['generate_password'];
}
 
$len = strlen($chars);
$pw = '';
 
for ($i=0;$i<$length;$i++)
        $pw .= substr($chars, rand(0, $len-1), 1);
 
// the finished password
$response = str_shuffle($pw);
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="robots" content="noindex">
    <title>Strong Password Generator - freewebmentor</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">
    <script src="https://code.jquery.com/jquery-1.10.2.min.js"></script>
    <script src="https://netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.min.js"></script>    
    <style>
    .bg-succes{padding:10px;}
  </style>
</head>
<body>
  <div class="container">
  <div style="margin-top:20px;"></div>
  <legend class="text-center text-primary">Strong Password Generator </legend>
  <form class="form-horizontal" method="post" id="csp" role="form">
    <fieldset>      
       <div class="form-group">
        <label class="col-sm-3 control-label" for="expirationMonth">Enter Password Length </label>
        <div class="col-sm-8">
          <div class="row">            
            <div class="col-xs-9">
              <input type="text" class="form-control" name="generate_password" required>
            </div>
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="col-sm-offset-3 col-sm-9">
          <button type="submit" name="submit" id="submit" class="btn btn-primary">Generate Password</button>
        </div>
         <br><br><br>
        <div class="col-sm-offset-3 col-sm-6">
        	<?php if(isset($response)){ ?><h4 class="text-success">Output: <textarea style="width: 100%;" disabled><?php echo $response; ?></textarea> <br><br>
        	<span class="text-warning">You need to copy using CTRL+C (Windows) and Command+C (Mac).</span></h4>
        </div>        
        <?php } ?>
      </div>
    </fieldset>
  </form>
  
</div>  
</body>
</html>
