```java
package model;

import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.UnsupportedEncodingException;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import com.google.gson.Gson;
import com.google.gson.JsonArray;
import com.google.gson.JsonObject;
import com.google.gson.stream.JsonReader;

public class BookParser {
	public List<BookInfo> getList(String title) {
		List<BookInfo> list = new ArrayList<>();


		JsonReader jr=null;
		HttpURLConnection con=null;
		try {
			URL url = new URL("https://app.rakuten.co.jp/services/api/BooksTotal/Search/20170404?format=json&keyword="
					+ title + "&booksGenreId=000&applicationId=1099249507950774425");
			con = (HttpURLConnection) url.openConnection();
			con.setRequestMethod("GET");
			InputStream is = con.getInputStream();
			InputStreamReader isr = new InputStreamReader(is, "UTF-8");
			jr = new JsonReader(isr);
			Gson gson = new Gson();
			JsonObject root = gson.fromJson(jr, JsonObject.class);
			JsonArray items = root.get("Items").getAsJsonArray();
			for(int i=0;i<items.size();i++){
				BookInfo book=new BookInfo();
				JsonObject obj=items.get(i).getAsJsonObject();
				JsonObject item=obj.get("Item").getAsJsonObject();
				book.setLargeImageUrl(item.get("largeImageUrl").getAsString());
				book.setTitle(item.get("title").getAsString());
				book.setAuthor(item.get("author").getAsString());
				book.setItemUrl(item.get("itemUrl").getAsString());
				list.add(book);
			}

		} catch (MalformedURLException e) {
			e.printStackTrace();
		} catch (UnsupportedEncodingException e) {
			// TODO 自動生成された catch ブロック
			e.printStackTrace();
		} catch (IOException e) {
			// TODO 自動生成された catch ブロック
			e.printStackTrace();
		} finally {
			if(jr != null){
				try {
					jr.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			if(con !=null){
				con.disconnect();
			}
		}
		return list;
	}
}
```
