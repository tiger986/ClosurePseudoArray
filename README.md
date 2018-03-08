# The use of closures and the transformation of pseudo array into arrays
#### `demand: Click the button to print its corresponding subscript`
#### HTML code
```html
<div>
    <p>0</p>
		<p>1</p>
		<p>2</p>
		<p>3</p>
		<p>4</p>
		<p>5</p>
		<p>6</p>
		<p>7</p>
		<p>8</p>
		<p>9</p>
</div>
#### JS code
```javascript
//error method
for(var i = 0; i <btns.length; i++){
    btns[i].onclick = function(){
		    console.log(i);
				/*Click on each button to print out 9, because this is just a definition of a function that is called when the button is                   clicked, and the cycle is already over: i=9*/
	  }
}

//method1
for(var i = 0; i <btns.length; i++){
		btns[i].index = i; //Save the corresponding I with the attribute of the button
		btns[i].onclick = function(){
		    console.log(this.index); //What is printed is the corresponding attribute value, equal to the corresponding I
			  //Click the button to call the function i=9, but we don't print I, but the corresponding index value that is stored
		}
}

//method2
for(var i = 0; i <btns.length; i++){
		(function(num){
		    btns[num].onclick = function(){				
			 	    console.log(num);
		    }
    })(i)
	  /*The function calls itself (called the anonymous function on the outer layer), and the loop is invoked once at a time. (every call         calls I into Num), so printing is the I value that comes out every time.*/
}

//method3
for(var i = 0; i < btns.length; i++){
		btns[i].onclick = (function(num){
		    return function(){
				    console.log(num);
			  }
		})(i) //The principle is the same, only the function of the call is different
}

//method4
btns = Array.prototype.slice.call(btns); //Convert a pseudo array into a real array		
//The forEach loop method can be used only by using a real array
btns.forEach(function(btn, index){ //btn is the corresponding button (P tag), and index is the subscript for the P tag
    btn.onclick = function(){
		    console.log(index); //Directly with the index parameter, this is the feature of the forEach cycle
		}
})
