<%@page import="java.util.Calendar"%>
<%@page import="java.time.Year" %>
<%@ page contentType="text/html; charset=UTF-8" %>
<%
		request.setCharacterEncoding("UTF-8");
		String userId = (String)session.getAttribute("userId");
		
		session.setMaxInactiveInterval(30);//10*60
		
		Calendar cal = Calendar.getInstance();
		
		//오늘 날짜 구하기
		int nowYear = cal.get(Calendar.YEAR);
		int nowMonth = cal.get(Calendar.MONTH)+1;
		int nowDay = cal.get(Calendar.DAY_OF_MONTH);
		
		//클라이언트에 의해 넘어온 데이터
		String strYear = request.getParameter("year");
		String strMonth = request.getParameter("month");
		
		int year = nowYear;
		int month = nowMonth;
		
		if(strYear!=null) {
			year = Integer.parseInt(strYear);	
		}
		if(strMonth!=null) {
			month = Integer.parseInt(strMonth);
		}
		int nextYear=year, nextMonth=month+1;
		if(nextMonth>12) {
			nextYear=year+1;
			nextMonth=1;
		}
		int preYear=year, preMonth=month-1;
		if(preMonth<1) {
			preYear=year-1;
			preMonth=12;
		}
		
		cal.set(year, month-1,1);
		int startDay = 1;
		int endDay = cal.getActualMaximum(Calendar.DAY_OF_MONTH);
		
		//year년 month월 1일의 주의수 구하기
		int week = cal.get(Calendar.DAY_OF_WEEK);
		
		
		
%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
<style type="text/css">
body {
	font-size: 12pt;
}
td {
	font-size: 12pt;
}
</style>

<script type="text/javascript">
	function sendIt() {
		
		var f = document.myForm;
		
		if(!f.userId.value) {
			alert("아이디를 입력!!");
			f.userId.focus();
			return;
		}
		if(!f.userPwd.value) {
			alert("패스워드를 입력!!");
			f.userPwd.focus();
			return;
		}
		
		f.action = "login_ok.jsp";
		f.submit();
	}
	  function day()
      {
          var f = document.forms[0];
          f.submit();
      }
</script>
</head>
<body>

<table border="1" width="600" align="center" style="font-size: 9pt;">
<tr height="20">
	<td colspan="2" align="right">
	|게시판|
	<%if(userId==null){%>
	일정관리
	<%}else{ %>
	<a href="schedule.jsp">일정관리</a>
	<%} %>
	|
	</td>
</tr>
<tr height="400">
	<td width="200" valign="top">
	
	<% if(userId==null) { %>
		<form action="" method="post" name="myForm">
		아이디:<input type="text" name="userId" size="10"/><br/>
		패스워드:<input type="password" name="userPwd" size="10"/><br/>
		<input type="button" value="로그인" onclick="sendIt();"/><br/>
		
		</form>
	
	<%}else{ %>
		<font color='blue'><%=userId %></font>님 환영..<br/>
		<a href="logout.jsp">로그아웃</a>
	<%} %>
	
	</td>
	<% if(userId==null) { %>
		<td valign="middle" align="center">
		<b>로그인하면 새로운 세상이 보입니다.</b>
		</td>
	<%}else{ %>
		<td >
<table align="center" width="210" cellpadding="2" cellspacing="1">
<tr>	
	<td align="center">
	 
	 <form action ="login.jsp" method="post">
	 
	<a href="login.jsp?year=<%=nowYear %>&month=<%=nowMonth %>">
	<img alt="today" src="./image1/today.jpg" align="left" width="40">
	</a>
	
	                <select name="year" onchange="day()">
                                    <%for(int i=year-5; i<year; i++) { %>
                                        <option value="<%=i%>" > <%=i%></option>
                                    <%} %>
                                    <option value="<%=year%>" selected="selected"><%=year%></option>
                                    <%for(int i=year+1; i<year+5; i++) { %>
                                        <option value="<%=i%>" > <%=i%></option>
                                    <%} %>
       
                            </select>
                           년
                            <select name="month" onchange="day()">
                                <% for(int i=1; i<=12; i++) {%>
                             <option value="<%=i%>" <%=month==i?"selected='selected'":"" %>> <%=i%> </option>
                                <%} %>
                            </select>
                               월
                        </form>
                    </td>
                </tr>
            </table>





<table align="center" width="210" cellpadding="0" cellspacing="1" bgcolor="#cccccc">
<tr>
	<td bgcolor="#e6e4e6" align="center"><font color="red">일</font></td>
	<td bgcolor="#e6e4e6" align="center">월</td>
	<td bgcolor="#e6e4e6" align="center">화</td>
	<td bgcolor="#e6e4e6" align="center">수</td>
	<td bgcolor="#e6e4e6" align="center">목</td>
	<td bgcolor="#e6e4e6" align="center">금</td>
	<td bgcolor="#e6e4e6" align="center"><font color="blue">토</font></td>
</tr>

<%
	int newLine = 0;
	out.print("<tr height='20'>");
	for(int i=1;i<week;i++) {
		out.print("<td bgcolor='#ffffff'>&nbsp;</td>");
		newLine++;
	}
	for(int i=startDay;i<=endDay;i++) {
		
		String fontColor = (newLine==0)?"red":(newLine==6)?"blue":"black";
		String bgColor = (nowYear==year)&&(nowMonth==month)
				&&(nowDay==i)?"#e6e4e6":"#ffffff";
		
		out.print("<td align='center' bgcolor='" + bgColor +
				"'><font color='" + fontColor + "'>" + i + "</font></td>");
		//<td align='center' bgcolor='#ffffff'><font color='black'>23</font></td>
		
		newLine++;
		
		if(newLine==7 && i!=endDay) {
			out.print("</tr><tr height='20'>");
			newLine = 0;
		}
	}
	while(newLine>0 && newLine<7) {
		out.print("<td bgcolor='#ffffff'>&nbsp;</td>");
		newLine++;
	}
	out.print("</tr>");
	%>
<%} %>

	
	</td >
</table>

</table>

</body>
</html>
