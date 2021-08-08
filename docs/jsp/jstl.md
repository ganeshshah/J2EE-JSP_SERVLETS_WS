# JSTL Reference

## JSTL taglib import 
``` JSP
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
```
## Include file (Java)

``` JSP
<%@ include file="/WEB-INF/jsp/common/date.jsp" %>
```

## Include file (JSP)
``` JSP
<jsp:include page="/WEB-INF/jsp/common/date.jsp">
	<jsp:param name="title" value="Date and Time"/>
</jsp:include>
```
## Import a URL
``` JSP
<c:import url="http://www.google.com">
	<jsp:param name="title" value="Google"/>
</c:import>
```
## Set a variable to be used within the page
``` JSP
<c:set var="title" value="Web Developmenent Blog"/>
This can be used inside the jsp page by calling ${title}
```

## For each loop

``` JSP
<c:forEach items="${result}" varStatus="status" var="item">
	${item.title}
</c:forEach>
```
## For each loop with a pre-determined limit

>Display the first 3 items
``` JSP
<c:forEach items="${result}" varStatus="status" 
var="item" begin="0" end="2">
	...
</c:forEach>
```
## Check if it is the last item in the loop
``` JSP
<c:forEach items="${items}" var="item" varStatus="status">
	${item}<c:if test="${not status.last}">, </c:if>
</c:forEach>
```
## If condition
``` JSP
<c:if test="${not empty title}">
	Title isn't empty
</c:if>
```

## Choose Statement
``` JSP
<c:choose>
   	<c:when test="${linkNameLen > 18}">
   		<c:set var='linkNameShort' value='${fn:substring(link.linkName, 0, 18)}...'/>
   	</c:when>
   	<c:otherwise>
    		<c:set var='linkNameShort' value='${link.linkName}'/>  				
   	</c:otherwise>
</c:choose>
```
## String Manipulation
### Display a subset of a string

>Display only the first 80 characters
``` JSP
${fn:substring(url, 0, 80)}
Count the total number of characters in a string

<c:if test="${fn:length(url) > 80}">...</c:if>
```
>Replace certain characters in a string
``` JSP
<c:set var="description" 
value="${fn:replace(string, 'Old Text', 'New Text')}" />
```
>Convert string to all lowercases
``` JSP
${fn:toLowerCase(string)}
```
>Check if a string contains certain value
``` JSP
<c:if test="${not empty param.gender && 
fn:contains(param.gender,'Female')}"> checked="checked"</c:if>
```
>Split a string into an array

>Eg: Split 14/10/2009
``` JSP
<c:set var="date" value="${fn:split(start_date, '/')}" />  
<c:set var="day" value="${date[0]}" />
<c:set var="month" value="${date[1]}" />
<c:set var="year" value="${date[2]}" />
```
>Check if a string starts with certain characters
``` JSP
<c:choose>
	<c:when test="${fn:startsWith(website,'http') }">
		<a href="${website}">${website}</a>
	</c:when>
	<c:otherwise>
		<a href="http://${website}">http://${website}</a>
	</c:otherwise>
</c:choose>
```
## Display text with html values escaped
``` JSP
<c:out value="${summary}"/>
```
## Display text with html values
``` JSP
<c:out value="${cat.name}" escapeXml="false"/>
```
## Escape html values (same result as using <c:out>)
``` JSP
${fn:escapeXml(summary)}
```
## Logical Operators
>OR operator
``` JSP
<c:if test="${(title == 'null') || (empty title)}">
	...
</c:if>
```
>AND operator
``` JSP
<c:if test="${(title != 'null') && (title == 'Page 1')}">
	...
</c:if>
```
## Mathematical operators

>Addition
``` JSP
<c:if test="${counter + 2 == 4}">
```
>Subtraction
``` JSP
<c:if test="${counter - 2 == 0}">
```
>Multiplication
``` JSP
<c:if test="${counter * 2 == 4}">
```
>Division
``` JSP
<c:if test="${counter / 2 == 4}">
```
>Remainder
``` JSP
<c:if test="${counter % 2 == 0}">
```
## Form a URL with parameters
``` JSP
<c:url value="http://www.google.com/search" var="google_search">
	<c:param name="q" value="web development blog"/>
	<c:param name="hl" value="en"/>
</c:url>
<c:out value="${google_search}"/>
```
## Check a parameter from URL
``` JSP
<c:if test="${param.name != 'null' && not empty param.name}">
	...
</c:if>
```
## Check session
``` JSP
<c:when test="${not empty sessionScope['javax.portlet.userinfo']}">
```
## Check if form is submitted
``` JSP
<c:if test="${pageContext.request.method == 'POST'}">
	...
</c:if>
``` 
# More references for JSTL
- [ Oracle DOcumentation for JSTL ](https://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/)

