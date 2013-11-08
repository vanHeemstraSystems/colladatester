#colladatester

Allows you to test your collada in Threejs. 

Supports colladas with or without textures.

Simply drag the collada and your textures files into the browser or by using the filemenu.

Check the [live example](http://abumarkub.org/colladatester).

Makes use of:

[Threejs](http://threejs.org)
[ColladaLoader](https://github.com/mrdoob/three.js/blob/master/examples/js/loaders/ColladaLoader.js)
[dat.gui](https://code.google.com/p/dat-gui/)


I made some small changes to the original ColladaLoader of [Tim Knip](http://techblog.floorplanner.com/).

```
#!javascript

// from line 124
if ( url !== undefined ) {

	var parts = url.split( '/' );
	parts.pop();
	baseUrl = ( parts.length < 1 ? '.' : parts.join( '/' ) ) + '/';

}

// changed to support calling ColladaLoader.parse() without url:
if ( url !== undefined) {

	var parts = url.split( '/' );
	parts.pop();
	baseUrl = ( parts.length < 1 ? '.' : parts.join( '/' ) ) + '/';

}else{
	baseUrl = '';
}

```

```
#!javascript

// on line 3168
	this.transparent.color.b)
	/ 3 * this.transparency;


// changed to prevent breaking the syntax highlighter in SublimeText:
	this.transparent.color.b) / 3 * this.transparency;
```

```
#!javascript

// on line 3202
if (image) {

	var texture = THREE.ImageUtils.loadTexture(baseUrl + image.init_from);
	texture.wrapS = cot.texOpts.wrapU ? THREE.RepeatWrapping : THREE.ClampToEdgeWrapping;
	texture.wrapT = cot.texOpts.wrapV ? THREE.RepeatWrapping : THREE.ClampToEdgeWrapping;
	texture.offset.x = cot.texOpts.offsetU;
	texture.offset.y = cot.texOpts.offsetV;
	texture.repeat.x = cot.texOpts.repeatU;
	texture.repeat.y = cot.texOpts.repeatV;
	props['map'] = texture;

	// Texture with baked lighting?
	if (prop === 'emission') props['emissive'] = 0xffffff;

}


// changed to support inline textures:
if (image) {
	
	var texture;

	if(image.init_from.indexOf('data:') === 0){
	
		var texture = new THREE.Texture();
		var img = new Image();
		img.src = image.init_from;
		texture.needsUpdate = true;									
	
	}else{
	
		texture = THREE.ImageUtils.loadTexture(baseUrl + image.init_from);
	}

	texture.image = img;
	texture.wrapS = cot.texOpts.wrapU ? THREE.RepeatWrapping : THREE.ClampToEdgeWrapping;
	texture.wrapT = cot.texOpts.wrapV ? THREE.RepeatWrapping : THREE.ClampToEdgeWrapping;
	texture.offset.x = cot.texOpts.offsetU;
	texture.offset.y = cot.texOpts.offsetV;
	texture.repeat.x = cot.texOpts.repeatU;
	texture.repeat.y = cot.texOpts.repeatV;
	props['map'] = texture;

	// Texture with baked lighting?
	if (prop === 'emission') props['emissive'] = 0xffffff;

}
```