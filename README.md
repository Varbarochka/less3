Skip to content
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@Varbarochka 
Learn Git and GitHub without any code!
Using the Hello World guide, you’ll start a branch, write comments, and open a pull request.


vladlen-vozhzhaev
/
0423_edu
1
00
 Code
 Issues 0
 Pull requests 0 Actions
 Projects 0
 Wiki
 Security 0
 Insights
Продолжаем писать бота 13.05.2020

1) Теперь программа работает на двух сайтах google и музыкалка.
2) Написали функцию ввода запроса по буквам.
3) Научили искать сайт не только на первой странице. (Бот ищет сайт до 10 странице поисковика)
4) Вынесли код поиска сайта на странице поисковика в отдельную функцию getGooglePage()
 master
@vladlen-vozhzhaev
vladlen-vozhzhaev committed 1 hour ago 
1 parent cb2025b commit 2e3216ccc0daa1a0c4ecec17932dde6c2d865768
Showing  with 41 additions and 8 deletions.
 49  bot_for_serfing/script.js 
@@ -5,6 +5,7 @@
// @description  try to take over the world!
// @author       You
// @match        https://www.google.com/*
// @match        https://xn----7sbab5aqcbiddtdj1e1g.xn--p1ai/*
// @grant        none
// ==/UserScript==

@@ -13,19 +14,51 @@ let keywords = ["Гобой", "Как звучит флейта", "Что так
let keyword  = keywords[getRandom(0,keywords.length)];

if (btnK!=undefined){
    document.getElementsByName('q')[0].value = keyword;
    setTimeout(()=>btnK.click(), getRandom(3000,10000));
    writeWord(keyword);
}

let links = document.links;
for(let i=0; i<links.length; i++){
    if(links[i].href.indexOf('xn----7sbab5aqcbiddtdj1e1g.xn--p1ai')!=-1){
        let link = links[i];
        setTimeout(()=>link.click(), getRandom(3000,10000));
        break;

if (location.host == "www.google.com"){
    getGooglePage();
}
else {
    if (getRandom(0,100)>20){
        let index = getRandom(0,links.length);
        if(links[index].href.indexOf('xn----7sbab5aqcbiddtdj1e1g.xn--p1ai')!=-1)
            setTimeout(()=>{links[index].click();},getRandom(3000, 10000));
        else location.href = 'https://xn----7sbab5aqcbiddtdj1e1g.xn--p1ai/';
    }
    else location.href = "https://www.google.com/";
}

function getRandom(min,max){
    return Math.floor(Math.random()*(max-min)+min);
}

function writeWord(keyword){
  let i = 0;
  let timerId = setInterval(()=>{
    document.getElementsByName('q')[0].value += keyword[i];
    i++;
    if (i==keyword.length) {
        clearInterval(timerId);
        btnK.click();
    }
  },300);
}

function getGooglePage(){
    let goNextPage = true;
    for(let i=0; i<links.length; i++){
        if(links[i].href.indexOf('xn----7sbab5aqcbiddtdj1e1g.xn--p1ai')!=-1){
            let link = links[i];
            goNextPage = false;
            setTimeout(()=>link.click(), getRandom(3000,10000));
            break;
        }
    }
    if (goNextPage) setTimeout(()=>{
        if (document.getElementsByClassName('YyVfkd')[0].innerText == 10) logo.click();
        else pnnext.click();
    }, getRandom(3000,10000));
}
0 comments on commit 2e3216c
@Varbarochka
 
 
Leave a comment

Attach files by dragging & dropping, selecting or pasting them.
 You’re not receiving notifications from this thread.
© 2020 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About

