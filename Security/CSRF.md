# CSRF
Cross-Site Request Forgery is an attack forces an end-user to execute unwanted actions on a web application in which they're currently authenticated.

## Scenario
### GET attack
If user clicks a button to see pictures and bank.com allows transfer with the request with query parameters, money will be transfered to the hacker and CSRF attack succeeded.

```html
<a href="http://bank.com/transfer.do?acct=MARIA&amount=100000">View my Pictures!</a>
```

### POST attack
```html
<body onload="document.forms[0].submit()">
  <form action="<nowiki>http://bank.com/transfer.do</nowiki>" method="POST">
  <input type="hidden" name="acct" value="MARIA"/>
  <input type="hidden" name="amount" value="100000"/>
  <input type="submit" value="View my pictures"/>
  </form>
  ...
</body>
```

This can be really happened if the server is not set [SOP](https://resources.infosecinstitute.com/bypassing-same-origin-policy-sop/#gref).
