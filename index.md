---
layout: default
title: "Internet Images"
---

<header>
  <h1>
    <span js-random-emoji></span>
    📂
    <span js-random-emoji></span>
  </h1>
  <small>
    International Image Folder
  </small>
</header>

<main js-random-image></main>

<script>
  // https://jekyllcodex.org/without-plugin/image-gallery

  var imagesList = [
    {% for file in site.static_files %}
      {% if file.path contains "/images/display" %}
        {% assign filenameparts = file.path | split: "/" %}
        {% assign filename = filenameparts | last | replace: file.extname,"" %}
        {
          path: '{{ site.url}}{{ file.path | relative_url }}',
          name: '{{ filename }}'
        },
      {% endif %}
    {% endfor %}
  ];

  var emojiList = [
    '🥺',
    '😩',
    '😵‍💫',
    '🥵',
    '🤧',
    '😶‍🌫️',
    '🤤',
    '🥴',
    '🤥',
    '🥸',
    '🤒',
  ];

  var selectRandom = function(array) {
    var min = Math.ceil(1);
    var max = Math.floor(array.length - 1);
    var random = Math.floor(Math.random() * (max - min + 1)) + min;
    console.log('index', random)
    return array[random];
  };

  var formatBackgroundImage = function(stringPath) {
    return 'url("' +stringPath+ '")';
  };

  document.addEventListener('DOMContentLoaded', function() {
    var elImage = document.querySelector('[js-random-image]');
    var elEmojiList = document.querySelectorAll('[js-random-emoji]');

    elImage.style.backgroundImage = formatBackgroundImage( selectRandom(imagesList).path );

    var randomEmoji = selectRandom(emojiList);
    elEmojiList.forEach(function(el) { el.innerText = randomEmoji });

    document.addEventListener('click', function() {
      elImage.style.backgroundImage = formatBackgroundImage( selectRandom(imagesList).path );

      var randomEmoji = selectRandom(emojiList);
      elEmojiList.forEach(function(el) { el.innerText = randomEmoji });
    });
  });
</script>
