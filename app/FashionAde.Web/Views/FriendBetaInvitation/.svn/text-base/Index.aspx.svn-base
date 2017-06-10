<%@ Page Language="C#" MasterPageFile="~/Views/Shared/Site.Master" AutoEventWireup="true" Inherits="System.Web.Mvc.ViewPage<BetaInvitation>" %>
<%@ Import Namespace="FashionAde.Web.Controllers.MVCInteraction"%>

<asp:Content ID="indexContent" ContentPlaceHolderID="MainContentPlaceHolder" runat="server">
<h1>Invite up to 5 friends to the Beta period</h1>

<p>Thank you for registering on Fashion-Ade.com. During this beta period you can invite up to 5 friends to share your outfits with.</p>
<p>Write their email addresses here:</p>
<% 
    Html.EnableClientValidation();

    using (Html.BeginForm())
    {
        for (int i = 0; i < Model.Emails.Length; i++)
        {
            Response.Write(Html.TextBoxFor(x => Model.Emails[i].EmailAddress));
            Response.Write(Html.ValidationMessageFor(x => Model.Emails[i].EmailAddress));
            Response.Write("<br><br>");
        }

        Response.Write(Html.TextBoxFor(x => Model.Comments));

        Response.Write(Html.ValidationSummary());
%>
    <input type="submit" name="submit" value="Invite Contacts" /> or <%= Html.ActionLink("Start using Fashion-Ade.com", "Index", "Home")%>
<%
    }
%>

</asp:Content>
<asp:Content ID="Content1" ContentPlaceHolderID="ScriptsPlaceHolder" runat="server">
<script type="text/javascript" src="/static/js/MicrosoftAjax.js"></script>
<script type="text/javascript" src="/static/js/MicrosoftMvcValidation.js"></script>
</asp:Content>