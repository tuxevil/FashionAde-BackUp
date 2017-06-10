<%@ Page Language="C#" MasterPageFile="~/Views/Shared/Site.Master" AutoEventWireup="true" Inherits="System.Web.Mvc.ViewPage" %>
<%@ Import Namespace="FashionAde.Web.Controllers.MVCInteraction"%>

<asp:Content ID="indexContent" ContentPlaceHolderID="MainContentPlaceHolder" runat="server">
    <h1>Forgot your password?</h1>
    
    <% using (Html.BeginForm("PasswordRecovery", "Login"))
    { %>
    <table style="width:410px; margin-left:auto; margin-right:auto; border:solid 1px #CBCBCB; -moz-border-radius: 3px; -webkit-border-radius: 3px;">
        <tr style="border-bottom:solid 1px #CBCBCB; height:60px;">
            <td style="text-align:right;">
                <span style="font-size:14px;">User Name:</span>
            </td>
            <td><%= Html.TextBox("Username", string.Empty, new { maxlength = 50 })%> </td>            
        </tr>
        <tr style="height:40px;">
            <td style="text-align:right;">
                <span style="color:#F39852; font-size:14px;">Secret question:</span>
            </td>
            <td>
                <span id="Question" style="color:#000;">Please type your user name...</span>
            </td>
        </tr>
        <tr style="height:35px;">
            <td style="text-align:right;">
                <span style="font-size:14px;">Answer:</span>
            </td>
            <td><%= Html.TextBox("Answer", string.Empty, new { maxlength = 50 })%> </td>
        </tr>
        <tr style="height:10px;"><td><td></td></td></tr>         
    </table>        
    
    <input id="SendAnswer" type="image" src="/static/img/LogIn/btnSend.jpg" value="Finish" style="margin:5px auto 5px auto; display:block;" />     
    <input type="hidden" id="UserName" name="UserName" />                    
    <% } %>


</asp:Content>
<asp:Content ID="Content1" ContentPlaceHolderID="ScriptsPlaceHolder" runat="server">
<script type="text/javascript">
    var isValid = false;
    
    $(document).ready(function() {
        $('#Username').blur(GetQuestion);  
        
        $("#SendAnswer").click(function(e){ 
            if(!isValid)
            {
                showMessage("That username doesn't exist.");
                return false;
            }
            else if($("#Answer").val() == "")
            {
                showMessage("Your answer is empty.");
                return false;
            }
        });
    });

    function GetQuestion() {
        temp = $("#Username").val().toString();

        var encoded = $.toJSON(temp);

        $.ajax({
            type: "POST",
            url: "<%= Url.RouteUrl(new { controller = "Login", action= "GetQuestion"}) %>",
            data: encoded,
            contentType: "application/json; charset=utf-8",
            dataType: "json",
            success: function(data) {                
                if(data.Exist == true){
                    isValid = true;
                    ShowQuestion(data.PasswordQuestion);                    
                }
                else
                {     
                    isValid = false;               
                    $("#Question").text("That username doesn't exist.").css("color", "red");
                    $("#Username").focus();
                }
            }
        });
    }

    function ShowQuestion(data) {
        $("#Question").text(data).css("color", "black");;
        $("#UserName").val($("#Username").val());        
        $("#Answer").focus();
    }

</script>
</asp:Content>