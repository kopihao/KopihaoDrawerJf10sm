# KopihaoDrawerJf10sm

_Nothing reinvent, merely utilize [jfeinstein10's sliding menu](https://github.com/jfeinstein10/SlidingMenu) ._

## Platform
- Android

## Why use this
1. Jeremy Feinstein's SlidingMenu (*hereinafter jf10sm*) is awesome
2. Souce code of jf10sm is included in this project
3. Lazier (*might not simpler, idk*) way to use slide menu
4. No need to understand jf10sm source code deeply

	_However, understand how to use jf10sm will help u to customize jf10sm at full potential_


## Why JF SlidingMenu
* Alternative to drawer layout
* Provide 'REVEAL' effect on sliding  [(see more)](http://demos.jquerymobile.com/1.4.5/panel)
* Competitive as jfeinstein10 SlidingMenu
* Left and right menu supported
* Left and right menu underlying below main view

## How it behave
1. Exactly as jf10sm.

## How to use
_Everything based on demo provided._ <br>

>#### Steps :
> 1. Copy src/everything under **com.view.plugin.jf10sm**
> 2. Copy res/values/jf10_sm_attrs.xml
> 3. Copy res/values/jf10_sm_ids
> 4. Define layout, explain later
> 5. Some code to be overwritten in your Activity, also..later...

---

_Left menu(*hereinafter LSM*) and Right menu(*hereinafter RSM*)_<br>


> ##### 3 layout to be defined in res/layout:
> 1. jf10sm - lay_jf10sm
> 2. left menu - lay_app_lsm
> 3. right menu -lay_app_rsm
> 4. main view - lay_app_template

> ##### Illustration:<br>
>|LSM|Main_View|RSM|<br>

 --- 
In your Activity class:

```java
	public void setContentView(int pLayid) {
		View pLayout = getLayoutInflater().inflate(R.layout.lay_app_template, null);
		super.setContentView(pLayout);
		mgrJF10SM = new JF10SMManager(this, new JF10SMConfig(this));
        
        //Here you set up LSM,RSM,MAINVIEW
		mgrJF10SM.setMainContent(pLayout);
		mgrJF10SM.setPrimaryMenu(R.layout.lay_app_lsm);
		mgrJF10SM.setSecondaryMenu(R.layout.lay_app_rsm);

		final View vAppContent = findViewById(R.id.vAppContent);
		if (vAppContent == null) {
			final String MSG_INCOMPATIBLE = "<Layout Incompact>\n"
					+ "Not compatible to app template, anomalies expected";
			popShortToast(MSG_INCOMPATIBLE);
			return;
		}

		if (pLayid != 0) {
			inflateUI(vAppContent, pLayid);
		}

		mgrJF10SM.getSlideMenu().setOnOpenedListener(new OnOpenedListener() {
			@Override
			public void onOpened() {
			}
		});

		mgrJF10SM.getSlideMenu().setOnCloseListener(new OnCloseListener() {
			@Override
			public void onClose() {
			}
		});

		//open main view
		mgrJF10SM.openMain();
        
        //enable swipe of both LSM, RSM
		enableSM(true, true); 
	}
```

What you do in code snippet above:
* tell JF10SMManager your layouts _(LSM, RSM, MainView)_
* configure with JF10SMConfig _(you may change the value inside)_
* inflate your current activity layout into app_template _(you might change the way setContentView() behave)_
* show MainView
* enable swipe for both LSM, RSM

```java
	public View findViewById(int id) {
		View v = super.findViewById(id);
		if (v == null) {
			// if can't be found
			return mgrJF10SM.getSlideMenu().findViewById(id);
		}
		return v;
	}

``` 
What you do in code snippet above:
* find your view by in layout (seek from jf10sm in case not found)

What JF10SMManager do:

|Action|How to|
|:---|:---|
|Open LSM | mgrJF10SM.openLeft()|
|Open RSM | mgrJF10SM.openRight()|
|Show Mainview | mgrJF10SM.openMain()|

## How to customize

### LAYOUT

Left menu(*hereinafter LSM*) and Right menu(*hereinafter RSM*) is designed as view group type, FrameLayout.

You may customize lsm (*lay_app_lsm in demo app*) and<br>
rsm (*lay_app_rsm in demo app*) according to your project requirement,
by
> **changing layout** (as ListView, GridView, etc)
>
> _OR_
>
> **inflate custom layout/fragment** into it.

<br><br>

### JF10SMConfig

It attempts to initialize jf10sm.

```java
    shawdowWidth = 10;
    menuWidth = ofDeviceWidth(pAct, 70);
    touchMargin = ofDeviceWidth(pAct, 20);
    fadeDegree = 0.35f;
    shadowResid = 0;
```
|Attribute|Value|
|:---|:---|
|shawdowWidth|shadow width of both LSM, RSM |
|shadowResid|shadow image of both LSM, RSM |
|fadeDegree|alpha of fading effect , <br> larger positive value will enable fade effect.<br> **BUT** value 0 will disable fade effect  | 
|menuWidth|menu width of both LSM, RSM | 
|touchMargin| touch sensitivity, <br> larger positive value will detect more swipe area from screen edge.<br> **OR** value 0 will detect whole screen <br> **OR** negative value will void swipe gesture|


You can initialize more jf10sm attributes via this and enhance method in JFSlideMenu
```java
	public void configure(JF10SMConfig pConfig) {
```

## Things to take note
- This project is build on latest version of jf10sm (last check 10/10/2015)
- Might not be maintained if jf10sm is updated by its author.
- Well, text me if you feel upgrade is needed, I will update when I'm free.

## Dependancy
_No string attached. Download and deploy._

## License

```
Copyright (C) 2015 Kopihao

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

 
