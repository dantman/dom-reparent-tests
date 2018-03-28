---
title: >
  Input focus
---

{% include header.html %}

<div id="demo">
	<input type="text" placeholder="A text input">
</div>
<div id="demo2"></div>

<p>The input will be automatically reparented every 3 seconds.</p>
<p id="countdown"></p>

<div id="buttons">
	Reparent using:<br>
	<input type="radio" name="reparent" value="direct" checked> appendChild<br>
	<input type="radio" name="reparent" value="detach"> removeChild + appendChild<br>
	<input type="radio" name="reparent" value="delay"> removeChild + wait + appendChild<br>
</div>

<script>
(function() {
{% include reparent.html %}
	function getReparentType() {
		for ( var i = 0; i < buttons.childNodes.length; ++i ) {
			var n = buttons.childNodes[i];
			if ( n.type === 'radio' && n.checked ) {
				return n.value;
			}
		}

		return 'direct';
	}

	var countdown = 3;
	function doCountdown() {
		countdown--;

		document.getElementById('countdown').textContent = countdown;

		if ( countdown <= 0 ) {
			countdown = 3;

			doReparent(reparent[getReparentType()]);
		}

		setTimeout(doCountdown, 1000);
	}
	doCountdown();
})();
</script>