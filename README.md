# Improved Bank Sinopac

## Auto Sign-In with Audio CAPTCHA
Link: https://accessibility.sinopac.com/MemberPortal/Member/aenv_Login.aspx

```js
const USER_ID = "YOUR_ID",
    USER_USERNAME = "YOUR_USERNAME",
    USER_PASSWORD = "YOUR_PASSWORD";
var PlayVoice = function () {
    var voiceTxt;
    $.ajax({
        url: "/Share/OnlineService/ValidateNumber.ashx?voice=voice&" + (new Date()).getTime(),
        type: "POST",
        dataType: "json",
        async: false,
        cache: false,
        controller: this,
        success: function (responseData) {
            if (responseData != null && responseData["result"] == "SUCCESS") {
                voiceTxt = responseData["voiceNum"];
                console.log(voiceTxt);
                document.forms[0].Captcha_Input.value = voiceTxt;
                document.querySelectorAll("input")[6].value = USER_ID;
                document.querySelectorAll("input")[7].value = USER_USERNAME;
                document.querySelectorAll("input")[8].value = USER_PASSWORD;
            }
        }
    });
    if (voiceTxt == null || voiceTxt == "") {
        alert("captchanotfound");
    }
}
PlayVoice();
document.querySelector("[alt=登入]").click();
```
