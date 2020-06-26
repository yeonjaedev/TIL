* JSP를 이용한 간단한 출력

Wildfly 19.0.0.Final 버전은 Configuration/standalone.xml에 이미 자동으로 deployment를 찾아주는 deployment-scanner가 subsystem으로 등록이 되어있는 상태.
// deployment-scanner 태그안에서 auto deploy exploded가 true 상태로 되있어야한다ㅏ.

따라서, 해야할 것은 /opt/wildfly/standalone/deployment/ 내에 war 어플리케이션 생성 후 그 안에 jsp파일만 작성해주면 된다. 그러면 자동으로 mapping해주어서 url끝에 jsp파일 이름만 넣어도 화면이 뜰 수 있다.

* 


[deployment/ROOT.war/DBtest.jsp]
```html
<%@ page import="java.sql.*" %>
<%@ page import="javax.sql.*" %>
<%@ page import="javax.naming.*" %>
<%@ page import="javax.rmi.*" %>
<%@ page import="java.rmi.*" %>
<%
try{
        Context ctx=new InitialContext();
        DataSource ds = (DataSource) ctx.lookup("jboss/postgresDataSource");  // 여기서 각자 설정한 postgresql datasource 경로를 정확히 적어줘야한다.
        Connection con = ds.getConnection();
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("select 1"); // select * from table_name으로 테스트해보는걸 추천.
        rs.next(); //결과의 다음줄
        out.println("Result is "+rs.getString(1)); //출력
        rs.close();
        con.close();
}catch(SQLException se){
        se.printStackTrace();
}
%>
```

Url 호출 = https://your-server-url:8080/DBtest.jsp

