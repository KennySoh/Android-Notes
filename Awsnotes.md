
## Code Pen

```js
var xhr=new XMLHttpRequest();
xhr.open('POST','https://12od33mwyb.execute-api.us-east-2.amazonaws.com/dev/compare-yourself')
xhr.onreadystatechange=function(event){
  console.log(event.target.response);
}
xhr.send();
```
