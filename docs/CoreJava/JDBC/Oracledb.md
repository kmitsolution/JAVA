```java
String jdbcurl="jdbc:oracle:thin:@localhost:1521:XE";
	String driver="oracle.jdbc.driver.OracleDriver";
	String username="system";
	String password="India123";
	Connection conn=null;
	Statement stmt= null;
	ResultSet rs=null;
	try
	{
		Class.forName(driver);
		conn = java.sql.DriverManager.getConnection(jdbcurl,username,password);
		stmt = conn.createStatement();
		String sql= "Select Sysdate from dual";
		rs =stmt.executeQuery(sql);
		if(rs.next()) {
			System.out.println(rs.getString("Sysdate"));
		}
	}catch(Exception ex)
	{
		throw new Exception(ex.getMessage());
	}
	}
```
