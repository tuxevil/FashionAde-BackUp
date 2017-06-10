<%@ Control Language="C#" AutoEventWireup="true" Inherits="System.Web.Mvc.ViewUserControl<List<SelectListItem>>" %>

<% if(Model.Count > 0 ){%>
<div style="float:right; left: -50%; position: relative;">
<div style="position: relative; left: 50%;">
    <ul style="display: inline;">
    <%
        foreach (SelectListItem item in Model)
        {
            if (!item.Selected)
            {
                %><li class="Page" id="<%= "page_" + item.Value %>"><%=item.Text%></li><%
            }
            else
            {
                %><li class="SelectedPage"><%=item.Text%></li><%
            }
        } %>
    </ul>
    </div>
</div><br />
<% } %>