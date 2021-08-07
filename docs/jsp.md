
# JSP Reference 
# Evaluate Java expression at run time
## Prototype 

```jsp
<%=     %>
```

## Example

```jsp
Current date : <%= new java.util.Date() %>
```

# Scriptlets

## Prototype 

```jsp
<%      %>
```

## Example

```jsp
<%
     System.out.println("Write in console log");
     out.println("write in : javax.servlet.jsp.JspWriter \"out \" variable <br>");
     java.util.Date date = new java.util.Date();
%>

<%
    if ( hello ) {
        %>
        <P>Hello, world at : <%= date %>
        <%
    } else {
        %>
        <P>Goodbye, world at : <%= date %>
        <%
    }
%>
```

# Directives

## Prototype 

```jsp
<%@     %>
```

## Example with a "page directive"

**Java library includes**

```jsp

<%@ page import="java.util.Date, java.util.ArrayList" %>

Current date : <%= new Date() %>
```

## Example with a "include directive"

**Physically include the contents of another file, HTML or JSP**

```jsp
<html>
        <body>
                include other.jsp...<BR>
                <%@ include file="other.jsp" %>
        </body>
</html>
```

# Declarations

**You can also add variable and method declarations to this class.  You can then use these variables and methods from your scriptlets and expressions.**

## Prototype 

```jsp
<%!     %>
```

## Example

**The date will be the same, no matter how often you reload the page.  This is because these are declarations, and will only be evaluated once when the page is loaded**

```jsp
<%!
    Date theDate = new Date();
    Date getDate()
    {
        System.out.println( "In getDate() method" );
        return theDate;
    }
%>
Hello!  The time is now <%= getDate() %>
```

# Tags

## Prototype

```jsp
        <some:tag>
                body
        </some:tag>
```

If the tag does not require a body, the start and end can be conveniently merged together, as

```jsp
<some:tag/>
```

## Example with include 

**jsp:include is similar.  But instead of loading the text of the included file in the original file, it actually calls the included target at run-time**

```jsp
<html>
        <body>
                Going to include hello.jsp...<BR>
                <jsp:include page="hello.jsp"/>
        </body>
</html>
```

# JSP session

## Prototype

```jsp
<%
        session.setAttribute(... , ...);
%>
```

## Example

```jsp
<%
        string name = request.getParameter("username");
        session.setAttribute("theName" , name);
%>

<html>
        <body>
                Hello, <%= session.getAttribute( "theName" ) %>
        </body>
</html>

```

# JSP bean

**You need first to declare java class that will be used as bean**

```java

package my.big.fat.package.name.as.folders.where.class.files.are.included;

public class UserData {

    private String username;
    private String email;
    private int age;

    public void setUsername( String username )
    {
        this.username = username;
    }

    public void setEmail( String email )
    {
        this.email = email;
    }

    public void setAge( int age )
    {
        this.age = age;
    }

    public String getUsername() 
    { 
    	return this.username; 
    }

    public String getEmail() 
    { 
    	return this.email; 
    }

    public int getAge() 
    { 
    	return this.age; 
    }

}
```

## Prototype

```jsp
<jsp:useBean id="userId" class="my.big.fat.package.name.as.folders.where.class.files.are.included.UserData" scope="session"/>
```

## Example

### getName.html

```html
<html>
	<body>
		<form METHOD=POST ACTION="SaveName.jsp">
		What's your name? <INPUT TYPE=TEXT NAME=username SIZE=20><BR>
		What's your e-mail address? <INPUT TYPE=TEXT NAME=email SIZE=20><BR>
		What's your age? <INPUT TYPE=TEXT NAME=age SIZE=4>
		<P><INPUT TYPE=SUBMIT>
		</form>
	</body>
</html>
```

### SaveName.jsp

```jsp
<jsp:useBean id="john" class="my.big.fat.package.name.as.folders.where.class.files.are.included.UserData" scope="session"/>
<jsp:setProperty name="john" property="*"/> 
<jsp:setProperty name="john" property="*"/> 

<html>
	<body>
		<a href="NextPage.jsp"> Continue </a>
	</body>
</html>
```

### NextPage.jsp

```jsp
<jsp:useBean id="john" class="my.big.fat.package.name.as.folders.where.class.files.are.included.UserData" scope="session"/> 

<html>
	<body>
		You entered<BR>
		Name: <%= john.getUsername() %><BR>
		Email: <%= john.getEmail() %><BR>
		Age: <%= john.getAge() %><BR>
	</body>
</html>
```
