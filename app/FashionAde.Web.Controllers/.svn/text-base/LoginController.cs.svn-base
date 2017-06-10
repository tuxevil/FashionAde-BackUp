using System;
using System.Collections.Generic;
using System.Web.Mvc;
using System.Web.Security;
using FashionAde.Core;
using FashionAde.Core.DataInterfaces;
using FashionAde.Web.Controllers.MVCInteraction;
using FashionAde.Core.Accounts;
using System.Web;
using FashionAde.Web.Common;
using FashionAde.ApplicationServices;

namespace FashionAde.Web.Controllers
{
    [HandleError]
    public class LoginController : BaseController
    {
        IRegisteredUserRepository registeredUserRepository;
        IMessageSenderService messageSender;

        public LoginController(IRegisteredUserRepository registeredUserRepository, IMessageSenderService messageSender)
        {
            this.registeredUserRepository = registeredUserRepository;
            this.messageSender = messageSender;
        }

        [AcceptVerbs(HttpVerbs.Get)]
        public ViewResult Index(string validatedUser)
        {
            ViewData["Errors"] = TempData["Errors"];
            TempData["Errors"] = null;
            ViewData["validatedUser"] = !string.IsNullOrEmpty(validatedUser) && Convert.ToBoolean(validatedUser);

            return View();
        }

        [AcceptVerbs(HttpVerbs.Post)]
        public RedirectToRouteResult Validate(string userName, string userPassword, bool? chkMaintain)
        {
            bool firstTime = false;
            MembershipUser mu = Membership.GetUser(userName);
            if (mu != null && mu.CreationDate == mu.LastLoginDate) {
                firstTime = true;
            }

            if (Membership.ValidateUser(userName, userPassword))
            {
                bool tmp = false;
                if (chkMaintain != null)
                    tmp = (bool) chkMaintain;

                FormsAuthentication.SetAuthCookie(userName, tmp);
                UserDataHelper.LoadFromDatabase(userName);

                // Clear closet state when the user logs in.
                new BuildYourClosetState().Clear();

                if (firstTime)
                    return RedirectToAction("Index", "FriendBetaInvitation");
                else
                    return RedirectToAction("Index", "Home");
            }
            else
            {
                TempData["Errors"] = "The username and password supplied are not valid.";
                return RedirectToAction("Index", "Login");
            }
        }

        public RedirectToRouteResult LogOut()
        {
            FormsAuthentication.SignOut();
            Session.Abandon();
            return RedirectToAction("Index", "Home");
        }

        [AcceptVerbs(HttpVerbs.Get)]
        public ViewResult ForgotPassword()
        {
            ViewData["Errors"] = TempData["Errors"];
            TempData["Errors"] = null;
            return View();
        }

        [ObjectFilter(Param = "username", RootType = typeof(string))]
        public ActionResult GetQuestion(string username)
        {
            MembershipUser mu = Membership.GetUser(username);
            if(mu != null)
            {
                if(mu.IsLockedOut)
                    mu.UnlockUser();
                return Json(new
                                {
                                    Exist = true,
                                    PasswordQuestion = mu.PasswordQuestion
                                });
                
            }

            return Json(new
            {
                Exist = false
            });
            
        }

        public RedirectToRouteResult PasswordRecovery(string UserName, string Answer)
        {
            MembershipUser mu = Membership.GetUser(UserName);

            try
            {
                PasswordEmailData ped = new PasswordEmailData();
                ped.UserName = mu.UserName;
                ped.NewPassword = Answer;
                messageSender.SendWithTemplate("forgotpassword", null, ped, mu.Email);
                TempData["Errors"] = "Your new password has been sent by email, please check your inbox.";
            }
            catch (Exception)
            {
                TempData["Errors"] = "Your answer dont match with the user answer.";
            }
           
            return RedirectToAction("Index");
        }
    }
}
