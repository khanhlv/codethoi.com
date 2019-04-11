+++
title = "Hưỡng dẫn tải toàn bộ ảnh trên Flickr về máy tính bằng Javascript"
description = "Hưỡng dẫn tải toàn bộ ảnh trên Flickr về máy tính bằng Javascript"
tags = ["flickr","javascript","code"]
keywords = ["flickr","javascript","code"]
date = "2019-04-11"
+++

Lướt mạng và xem ảnh gái, thấy flickr của 1 bạn Hiến Đặng toàn ảnh gái đẹp và hình sexy, nên muốn lấy toàn bộ của bạn ý về xem cho đơ lag và zoom xem có lộ hàng gì không =))

Link Flickr của Hiến Đặng
```
https://www.flickr.com/photos/125742869@N04/
```

Thử xem qua flickr của anh ấy xem nào

![Flickr Hiến Đặng](/images/04112019/flickr_1.jpg)

Toàn hàng hót và đẹp nhỉ, giờ tìm cách download thôi

Thử F12 (Chế độ Develop của trình duyệt) xem có gì làm ăn được gì không.

![Flickr Hiến Đặng](/images/04112019/flickr_2.jpg)

Á có API rồi, vậy thì đơn giản hơn rồi
```
https://api.flickr.com/services/rest?per_page=25&page=5&extras=can_addmeta,can_comment,can_download,can_share,contact,count_comments,count_faves,count_views,date_taken,date_upload,description,icon_urls_deep,isfavorite,ispro,license,media,needs_interstitial,owner_name,owner_datecreate,path_alias,realname,rotation,safety_level,secret_k,secret_h,url_c,url_f,url_h,url_k,url_l,url_m,url_n,url_o,url_q,url_s,url_sq,url_t,url_z,visibility,visibility_source,o_dims,publiceditability&get_user_info=1&jump_to=&user_id=125742869@N04&view_as=use_pref&sort=use_pref&viewerNSID=&method=flickr.people.getPhotos&csrf=&api_key=7a02be0302d61adc837e4f95655fc024&format=json&hermes=1&hermesClient=1&reqId=025caa42&nojsoncallback=1
```

Cùng phân tích tham số nào

1. **per_page=25**              -> Số item sẽ được hiển thị
2. **page=5**                   -> Số trang
3. **user_id=125742869@N04**    -> ID của bác hiến đặng
4. **api_key=7a02be0302d61adc837e4f95655fc024** -> Cái này quan trọng nhe, không có cái này thì API này không hoạt động

Bây giờ code HTML và Javascript để download nào

```
<html>
<head>
	<title>Download Image To Flickr</title>
</head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<body>
	<script>
		var makeUrl = function(page) {
			var user_id = $('input[name=user_id]').val();
			var api_key = $('input[name=api_key]').val();
			var url = 'https://api.flickr.com/services/rest?per_page=500&page=' + page + '&extras=can_addmeta,can_comment,can_download,can_share,contact,count_comments,count_faves,count_views,date_taken,date_upload,description,icon_urls_deep,isfavorite,ispro,license,media,needs_interstitial,owner_name,owner_datecreate,path_alias,realname,rotation,safety_level,secret_k,secret_h,url_c,url_f,url_h,url_k,url_l,url_m,url_n,url_o,url_q,url_s,url_sq,url_t,url_z,visibility,visibility_source,o_dims,is_marketplace_printable,is_marketplace_licensable,publiceditability&get_user_info=1&jump_to=&user_id='+ user_id +'&view_as=use_pref&sort=use_pref&viewerNSID=&method=flickr.people.getPhotos&csrf=&api_key='+ api_key +'&format=json&hermes=1&hermesClient=1&reqId=37913745&nojsoncallback=1';
			
			return url;
		}
		
		var download = function() {
			$.ajax({
				url: makeUrl(1),
			    type: 'GET',
				async: false,
			    success: function(data) {
					if (data.stat == 'ok') {
						var photo = data.photos.photo;
						var lengPhoto = photo.length;
						var pages = data.photos.pages;

						$('#total').html(data.photos.total);
						$('#pages').html(data.photos.pages);
						$('#page').html(1);
					
						for (var i = 0; i < lengPhoto; i++) {
							var item = photo[i];
							$('textarea[name=data_output]').append(item.url_k_cdn + '\n');
						}
						downloadPage(pages);
					}
				}
			});
		}
		
		var downloadPage = function(pages) {
			for (var p = 2; p <= pages; p++) {
				$('#page').html(p);
				$.ajax({
					url: makeUrl(p),
					type: 'GET',
					async: false,
					success: function(data) {
						if (data.stat == 'ok') {
							var photo = data.photos.photo;
							var lengPhoto = photo.length;
							for (var i = 0; i < lengPhoto; i++) {
								var item = photo[i];
								$('textarea[name=data_output]').append(item.url_k_cdn + '\n');
							}
						}
					}
				});
			}
		}
	</script>
	UserID: <input type="text" name="user_id" value="125742869@N04" /> <br><br>
	APIKey: <input type="text" name="api_key" value="7a02be0302d61adc837e4f95655fc024" /> <br><br>
	<button type="button" onclick="download()">Download</button><br><br>
	Total: <b id="total"></b><br><br>
	Pages: <b id="page"></b>/<b id="pages"></b><br><br>
	<textarea name="data_output" cols="90" rows="20"></textarea>
</body>
</html>
```

Lưu ra file HTML và chạy và nhận thành quả nào


