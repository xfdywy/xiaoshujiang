---
title:  手动输入网易云音乐歌单创建hexo 音乐播放器
date: 2018-5-6
tags:
    -   hexo 
    -   aplayer
    -   网易云音乐api
categories:  web
---


先挖个坑。欢迎点击左边的  `Music`来看看效果。也可以用这个链接[https://wyue.name/music/](https://wyue.name/music/)

已经实现了的是在hexo博客上，搞一个音乐播放器。
播放器选的是aplayer。
通过输入网易云音乐的歌单id，来创建播放列表。可以手动输入歌单id。

提前感谢各位大佬给的网易云音乐api。

学习到的几点：
## javascript http get 请求处理
## javascript json 处理
## javascript function 循环等
## 简单css


code 如下


``` html
---
title: 音乐
date: 2018-2-15 22:32:22
type: "music"
fancybox: True
comments: false
---

<link href="https://cdn.bootcss.com/aplayer/1.10.1/APlayer.min.css" rel="stylesheet">
<script src="https://cdn.bootcss.com/aplayer/1.10.1/APlayer.min.js"></script>


<div class="change_playlist">
网易云playlist id: <input id="playlist" value='2215356763' ><input id="nodeGoto" type="button"   onClick="showplaylist()"  value = 'change playlist'  />
</div>

<div id="player1" class="aplayer"></div>


# 推荐的网易云playlist
```
327073149
82292832
2215356763
```
<!-- <div class="instagram">
    <section class="archives album">
      <ul class="img-box-ul">
      </ul>
    </section>
</div>
 -->



<style type="text/css">
  #playlist {
      width: 40%;
      font-size: 16px;
      /*text-indent: 16px;*/

      text-align: center;
  }
    #nodeGoto {
    width: 20%;
    color: #222;
    font-size: 16px;
    height: 40px
    text-align: center;
    background: #b7daff;
    border: solid 2px #b7daff;
    cursor: pointer;
  }
    #playlist, #nodeGoto {
    /*float: left;*/
    outline: none;
    height: 38px;
    border: solid 1px #b7daff;
    padding: 0;
    line-height: 38px;
}
}

</style>

 

<script type="text/javascript">
	function downloadrul(id){
		// var url =  "https://api.imjad.cn/cloudmusic/?type=url&id=" +  id
		var url = "https://api.a632079.me/nm/url/" + id
    	var xmlHttp = new XMLHttpRequest();
		xmlHttp.open( "GET", url, false ); // false for synchronous request
		xmlHttp.send( null );
		var res =  JSON.parse(xmlHttp.responseText);
		var url = res.data[0].url;
		// var picurl  = res.songs[0].al.picUrl;
		// var artist = res.songs[0].ar[0].name;
		return(url);

	}


	function downloadlry(id){
		var url =  "https://api.imjad.cn/cloudmusic/?type=lyric&id=" +  id
    	var xmlHttp = new XMLHttpRequest();
		xmlHttp.open( "GET", url, false ); // false for synchronous request
		xmlHttp.send( null );
		var res =  JSON.parse(xmlHttp.responseText);
		if  ("nolyric" in res){
			var lrc = 'None';
		}
		else{
					var lrc = res.lrc.lyric;
		}

		return(lrc);
	}


	function downloadname(id){ 
		var url =  "https://api.imjad.cn/cloudmusic/?type=detail&id=" +  id
    	var xmlHttp = new XMLHttpRequest();
		xmlHttp.open( "GET", url, false ); // false for synchronous request
		xmlHttp.send( null );
		var res =  JSON.parse(xmlHttp.responseText);
		var name = res.songs[0].name;
		var picurl  = res.songs[0].al.picUrl;
		var artist = res.songs[0].ar[0].name;
		return([name , picurl , artist]);
	}

	function downloadplaylist(id){
		var url =  "https://api.imjad.cn/cloudmusic/?type=playlist&id=" +  id;
		var xmlHttp = new XMLHttpRequest();
		xmlHttp.open( "GET", url, false ); // false for synchronous request
		xmlHttp.send( null );
		var res =  JSON.parse(xmlHttp.responseText);
		var id_list =[];
		for (ii in res.playlist.tracks){
			id_list.push(res.playlist.tracks[ii].id.toString());
		}
		return(id_list) ;
	}

    function loadplaylist(playlistid){
      // '2215356763'
      var arr = downloadplaylist(playlistid)
      // var aa = "http://music.163.com/song/media/outer/url?id="
      var aa = 'https://api.a632079.me/nm/redirect/music/'
      bb = []
      for(i in arr){
        // alert(i)
        var detail = downloadname(arr[i])
        var lrc = downloadlry(arr[i])
        // var url = downloadrul(arr[i])
        // var url = aa + arr[i] +'.mp3'
        var url = aa+arr[i]
        // alert(lrc)
        temp = {
              name: detail[0],
                  artist: detail[2],
                  url: url,
                  cover:  detail[1], 
                  lrc: lrc,
                }
        bb.push(temp)
        }
        return(bb)
      }
</script>
 
<script type="text/javascript">  

  function showplaylist(){
      var input = document.getElementById("playlist");
      var bb = loadplaylist(input.value) ;
    // alert(bb);
       const ap = new APlayer({
          container: document.getElementById('player1'),
          fixed: false,
          lrcType: 1,
          audio: bb
            });
  };

    showplaylist();
 	</script>


```

