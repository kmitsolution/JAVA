### Step1 Create the WEB Project using Maven
1. Configure Tomcat Server for your project
2. Run the project and index.jsp should return Hello World
3. Let's Change the index.jsp ( validate user name )

```html
<!DOCTYPE html>
<html>
<head>
<script>
function myFunction() {
  var uname=document.getElementById("uname").value;
  //alert(uname.length);
  if( uname.length==0)
	  {
	  alert("user name cannot be blank");
	  return false;
	  }
  if(uname=="xyz")
	  {
	  alert("Authorized user");
	  }
  else
	  alert("Unauthrorized user");
}
</script>
</head>
<body>
 Username : <input type="text" id="uname" name="uname" > <br />
 Password : <input type="password" id="pass" name="pass" > <br />
 
 <input type="submit" onclick="myFunction()">
</body>
</html>
```
