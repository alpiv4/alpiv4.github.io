---
layout: default
title: Games
permalink: /games/
---

# Games

My free indie games. Play them right here or check them out on [itch.io](https://alpiv4.itch.io/). Leave Feedback!

---

WIP

<div id="itch-embed-container"></div>
<script>
(function() {
  var lightSrc = "https://itch.io/embed/4846281";
  var darkSrc = "https://itch.io/embed/4846281?bg_color=000000&fg_color=eeeeee&link_color=fa5c5c&border_color=000000";

  var container = document.getElementById('itch-embed-container');

  function renderEmbed() {
    var isDark = document.body.classList.contains('dark-mode');
    var src = isDark ? darkSrc : lightSrc;
    container.innerHTML = '<iframe frameborder="0" src="' + src + '" width="552" height="167"><a href="https://alpiv4.itch.io/frogjam">Webtest by alpiv4</a></iframe>';
  }

  renderEmbed();

  document.querySelector('.theme-toggle').addEventListener('click', function() {
    // Wait a tick so body.className has already been updated by the existing toggle handler
    setTimeout(renderEmbed, 0);
  });
})();
</script>

[https://alpiv4.itch.io/frogjam](https://alpiv4.itch.io/frogjam)

To play/test enter: frogster