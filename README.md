Fresh8 Android SDK
==================

## Introduction

The Fresh8 Android SDK will integrate Fresh8s content aware Ad serving platform into your android apps.

                
## Integration

1. Copy fresh8SDK.jar into your libs directory.
    
2. Add following permissions and activity declaration to your AndroidManifest.xml:

    ```<uses-permission android:name="android.permission.INTERNET"></uses-permission>```
    
    ```<activity android:name="com.fresh8.sdk.BetPageActivity" />```

3. Add fresh8SDK.jar to your projects Java build path

    In Eclipse:
    1. YourProject -> Properties
    2. Select Java Build Paths
    3. Select the Libraries tab
    4. Click on 'Add Jars...'
    5. Select fresh8SDK.jar from inside your libs folder
    6. Click 'Ok'

4. Fresh8 includes custom animations for viewing external betting pages. To include these animations copy the contents of the animation folder into you own `/res/anim/` folder
    
    

### Displaying ads
Fresh8 can be used for both article views and match page views:


1. In your Page view activity:

    1. Import Fresh8: `import com.fresh8.sdk.Fresh8;`
    
    2. Create Ad Banner Webview programmically to contain the fresh8 advert In your `-onCreate()` method
    
          ```
          WebView webView = new WebView(this);
        	//Create banner height relative to screen
		final int height = (int)TypedValue.applyDimension(TypedValue.COMPLEX_UNIT_DIP, 50, this.getResources().getDisplayMetrics());
        RelativeLayout.LayoutParams webViewParams= new RelativeLayout.LayoutParams(LayoutParams.FILL_PARENT, height);
        webViewParams.addRule(RelativeLayout.ALIGN_PARENT_BOTTOM);
        webViewParams.addRule(RelativeLayout.ALIGN_PARENT_RIGHT);
        
        RelativeLayout rL = new RelativeLayout(this);
        RelativeLayout.LayoutParams rLParams= new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.WRAP_CONTENT, RelativeLayout.LayoutParams.WRAP_CONTENT);
        rLParams.addRule(RelativeLayout.ALIGN_PARENT_BOTTOM);
        
        rL.addView(webView, webViewParams);
        addContentView(rL, rLParams);
		```


   3. Show banner ad in either your article or match page view:
        
        1. For article view pages you will need to create and array of content to be classified.
            ```String content[] = {"Article Title", "Article Body"};```
            
            Call the `Fresh9.presentAdBannerInView()` function
            
            ```
            Fresh8.presentAdBannerInView(this, content, fresh8WebView, new Handler() {
    			      @Override
          			public void handleMessage(Message msg) {
          				Boolean success = (Boolean) msg.obj;
          				if (success){
          					  // If a related bet has been found the message of true will be returned
          				} else {
          					  // A response of false will be returned if no related bet has been found
          				}
          			}
          		});
            ```
            
        2. For views related to a specific match, in order for fresh8 to be more precise you can pass through team names seperately, only returning bets related to the specified match
            `String homeTeam = "Arsenal"`
            `String awayTeam = "Everton"`
            `String league = "Premier league"`


            Call the `Fresh9.presentAdBannerInMatchView()` function
            
            ```
            Fresh8.presentAdBannerInMatchView(this, homeTeam, awayTeam, league, fresh8WebView, new Handler() {
        			@Override
        			public void handleMessage(Message msg) {
        				Boolean success = (Boolean) msg.obj;
        				if (success){
          				// If a related bet has been found the message of true will be returned
        				} else {
          				// A response of false will be returned if no related bet has been found
        				}
        			}
        		});
            ```
        
    
    ### Favourites

	If your app users are able to select their favourite teams to follow, this can be set in our SDK to help us in finding bets. It's not essential but will help us to provide bets related to your users favourtite teams if an article or match page cannot be matched to a bet.
   

	1.  To initiate the fresh8SDK with already favourited teams
	  
	    1. Import Fresh8: `import com.fresh8.sdk.Fresh8;`
	`
	            
	    2. If your users have favourite teams create an array of favourite names
	
	        `String[] favourites = { "Everton", "Chelsea" };`
	  
	  
	  
	    3. Initiate fresh8 with the users favourite teams, this can be used to help find related bets to the user.
	    
	        `Fresh8.initWithFavourites(favourites);`
	        
	    4. If there are no favourites this can be be left out.
    
	2. To Add newly favourited teams:
	        
	        `String favourite = "Everton"`;
	
	        `Fresh8.addFavourite(favourite);`


## Additional Features

### Debug Mode
    
    To assist in debugging
    
    `Fresh8.enableDebugLogging(true);`



