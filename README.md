# WH0818
# index.php
<?php 

    session_start();
    if (isset($_SESSION["userName"]))//檢查是否有資料
    
    $sUserName = $_SESSION["userName"];//有
    else 
    $sUserName = "Guest";//沒有

?>

# login.php
- 1.
    session_start();
    if (isset($_GET["logout"]))//read ? back things(index 28)
    {
    $_SESSION["userName"] = $sUserName;
    unset($_SESSION["userName"]);
    //setcookie("userName ", "Guest", time() - 3600);//clien cookie,-60*60*24*7 after 7 days ago can't eat
        header("Location: index.php");//go back to homepage
        exit();
    }

- 2.
    if (isset($_POST["btnOK"]))//read 表單，去看$_POST裏頭有沒有一個較btnOK的
    {
    //有
        $sUserName = $_POST["txtUserName"];//$sUserName(變數)<-["txtUserName"](帳號)，使用者寫入的帳號以陣列傳給sUN變數
        if (trim($sUserName) != "")//變數值不是空的時後
        {
        //不是
        
    // setcookie("userName", $sUserName);//請瀏覽器(userName)幫忙記住$sUserName的資料
        session_start();
        $_SESSION["userName"] = $sUserName;
        if (isset($_SESSION["lastPage"]))//read cookie，
        
            header(sprintf("Location: %s", $_SESSION["lastPage"]));//%s(字串)<-$_SESSION["lastPage"]，
            else
            header("Location: index.php");//go back to homepage
            exit();
        }
        
    }

# secret.php

<?php 
    session_start();
    if (!isset($_SESSION["userName"]))//檢查$_COOKIE是否沒有一個userName的陣列資料
    {
    //沒有
    $_SESSION["lastPage"] = "secret.php";
        setcookie("lastPage", "secret.php");//請瀏覽器(userName)幫忙記住$sUserName的資料
        header("Location: login.php");//回首頁
        exit();
        
    }

?>
