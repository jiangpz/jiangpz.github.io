---
layout: post
title:  "Stacked Regressions-Top 4% on LeaderBoard"
excerpt: "Kaggle House Prices 使用Stacking预测房价"
date:   2018-09-12 09:01:08 +0800
categories: Kaggle
tags: [Kaggle, Modeling, Stacking]
comments: true
---
<html>
<head><meta charset="utf-8" />
<title>Stacked Regressions-Top 4% on LeaderBoard</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.7 (http://getbootstrap.com)
 * Copyright 2011-2016 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    color: #000 !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=1);
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=3);
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
@media (max-width: 991px) {
  #ipython_notebook {
    margin-left: 10px;
  }
}
[dir="rtl"] #ipython_notebook {
  float: right !important;
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#login_widget {
  float: right;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  text-align: center;
  vertical-align: middle;
  display: inline;
  opacity: 0;
  z-index: 2;
  width: 12ex;
  margin-right: -12ex;
}
.alternate_upload .btn-upload {
  height: 22px;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
[dir="rtl"] #tabs li {
  float: right;
}
ul#tabs {
  margin-bottom: 4px;
}
[dir="rtl"] ul#tabs {
  margin-right: 0px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
[dir="rtl"] .list_toolbar .tree-buttons {
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-right {
  padding-top: 1px;
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-left {
  float: right !important;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: baseline;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
#tree-selector {
  padding-right: 0px;
}
[dir="rtl"] #tree-selector a {
  float: right;
}
#button-select-all {
  min-width: 50px;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
[dir="rtl"] #new-menu {
  text-align: right;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
[dir="rtl"] #running .col-sm-8 {
  float: right !important;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI colors. */
.ansibold {
  font-weight: bold;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  border-left-width: 1px;
  padding-left: 5px;
  background: linear-gradient(to right, transparent -40px, transparent 1px, transparent 1px, transparent 100%);
}
div.cell.jupyter-soft-selected {
  border-left-color: #90CAF9;
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected {
  border-color: #ababab;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 5px, transparent 5px, transparent 100%);
}
@media print {
  div.cell.selected {
    border-color: transparent;
  }
}
div.cell.selected.jupyter-soft-selected {
  border-left-width: 0;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 7px, #E3F2FD 7px, #E3F2FD 100%);
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #66BB6A -40px, #66BB6A 5px, transparent 5px, transparent 100%);
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  min-width: 0;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  padding: 0.4em;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. We need the 0 value because of how we size */
  /* .CodeMirror-lines */
  padding: 0;
  border: 0;
  border-radius: 0;
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul {
  list-style: disc;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ul ul {
  list-style: square;
  margin: 0em 2em;
}
.rendered_html ul ul ul {
  list-style: circle;
  margin: 0em 2em;
}
.rendered_html ol {
  list-style: decimal;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
  margin: 0em 2em;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  background-color: #fff;
  color: #000;
  font-size: 100%;
  padding: 0px;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  border: 1px solid black;
  border-collapse: collapse;
  margin: 1em 2em;
}
.rendered_html td,
.rendered_html th {
  text-align: left;
  vertical-align: middle;
  padding: 4px;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget {
  float: right !important;
  float: right;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 21ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  margin-top: 6px;
}
span.save_widget span.filename {
  height: 1em;
  line-height: 1em;
  padding: 3px;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  display: none;
}
.command-shortcut:before {
  content: "(command)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  width: 100%;
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal .xterm-rows {
  padding: 10px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sa { color: #BA2121 } /* Literal.String.Affix */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .dl { color: #BA2121 } /* Literal.String.Delimiter */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .fm { color: #0000FF } /* Name.Function.Magic */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .vm { color: #19177C } /* Name.Variable.Magic */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>原文地址：<a href="https://www.kaggle.com/serigne/stacked-regressions-top-4-on-leaderboard">https://www.kaggle.com/serigne/stacked-regressions-top-4-on-leaderboard</a></p>
<h1 id="Stacked-Regressions-to-predict-House-Prices">Stacked Regressions to predict House Prices<a class="anchor-link" href="#Stacked-Regressions-to-predict-House-Prices">&#182;</a></h1><h2 id="Serigne">Serigne<a class="anchor-link" href="#Serigne">&#182;</a></h2><p><strong>July 2017</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>这个比赛题目对我来说非常重要，因为它帮助我几个月前开始了我的Kaggle之旅。我在这里读过一些很棒的笔记本。仅举几例：</p>
<ol>
<li><p><a href="https://www.kaggle.com/pmarcelino/comprehensive-data-exploration-with-python">Comprehensive data exploration with Python</a> by <strong>Pedro Marcelino</strong>  : 十分好的数据分析（<a href="https://jiangpz.github.io/articles/2018-08/Examining-Your-Data）">https://jiangpz.github.io/articles/2018-08/Examining-Your-Data）</a></p>
</li>
<li><p><a href="https://www.kaggle.com/juliencs/a-study-on-regression-applied-to-the-ames-dataset">A study on Regression applied to the Ames dataset</a> by <strong>Julien Cohen-Solal</strong>  : 彻底的特征工程和对线性回归分析的深入研究，同时对初学者来说非常容易理解。（<a href="https://jiangpz.github.io/articles/2018-08/Preprocessing-By-Linear-Regression）">https://jiangpz.github.io/articles/2018-08/Preprocessing-By-Linear-Regression）</a></p>
</li>
<li><p><a href="https://www.kaggle.com/apapiu/regularized-linear-models">Regularized Linear Models</a> by <strong>Alexandru Papiu</strong>  :关于建模和交叉验证的Kernel（<a href="https://jiangpz.github.io/articles/2018-08/Regularized-Linear-Models-Xgboost-Keras）">https://jiangpz.github.io/articles/2018-08/Regularized-Linear-Models-Xgboost-Keras）</a></p>
</li>
</ol>
<p>我十分建议每个初学者都要仔细研究这些内核（当然还要通过其他很多内核）并获得他们在数据科学和Kaggle比赛中的第一次认识。</p>
<p>在那之后（以及一些基本的实践），你会更有信心理解 <strong>Human Analog</strong> 的<a href="https://www.kaggle.com/humananalog/xgboost-lasso">https://www.kaggle.com/humananalog/xgboost-lasso</a> 他做了令人印象深刻的功能改造工作。</p>
<p>由于数据集特别方便，我几天前决定回到本次比赛并应用我迄今学到的东西，特别是stacking模型。为此，我们构建了两个stacking类（最简单的方法和不太简单的方法）。</p>
<p>由于这些类是为通用目的而编写的，因此您可以轻松地调整它们和/或扩展它们以应对回归问题。希望这个方法简洁易懂。</p>
<p>特征工程很简单 :</p>
<ul>
<li><p><strong>Imputing missing values</strong>  by proceeding sequentially through the data</p>
</li>
<li><p><strong>Transforming</strong> 将一些看似数值型但是是表示种类的做转换</p>
</li>
<li><p><strong>Label Encoding</strong> 一些分类变量实际上包含了顺序信息</p>
</li>
<li><p><a href="http://onlinestatbook.com/2/transformations/box-cox.html"><strong>Box Cox Transformation</strong></a> 通过Box Cox Transformation处理偏态 (而不是做对数变换) : 这在排行榜和交叉验证方面给了我一个稍好的结果。</p>
</li>
<li><p><strong>Getting dummy variables</strong> 处理哑变量.</p>
</li>
</ul>
<p>接着我们选择一些基本模型 (主要是 sklearn 基本模型 + sklearn API of  DMLC's <a href="https://github.com/dmlc/xgboost">XGBoost</a> and 微软的 <a href="https://github.com/Microsoft/LightGBM">LightGBM</a>), 在 stacking/ensembling 他们之前做交叉验证. 这里的关键是使（线性）模型对异常值具有鲁棒性。这提高了LB排名和交叉验证的结果。</p>
<p>令我惊讶的是，这在LB上很好 ( 0.11420 and top 4% the last time I tested it : <strong>July 2, 2017</strong> )</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>希望当你看完这篇文章，你能理解stacking这个概念，虽然以前我们认为这个概念不容易理解</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#import some necessary librairies</span>

<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span> <span class="c1"># linear algebra</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span> <span class="c1"># data processing, CSV file I/O (e.g. pd.read_csv)</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>  <span class="c1"># Matlab-style plotting</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="n">color</span> <span class="o">=</span> <span class="n">sns</span><span class="o">.</span><span class="n">color_palette</span><span class="p">()</span>
<span class="n">sns</span><span class="o">.</span><span class="n">set_style</span><span class="p">(</span><span class="s1">&#39;darkgrid&#39;</span><span class="p">)</span>
<span class="kn">import</span> <span class="nn">warnings</span>
<span class="k">def</span> <span class="nf">ignore_warn</span><span class="p">(</span><span class="o">*</span><span class="n">args</span><span class="p">,</span> <span class="o">**</span><span class="n">kwargs</span><span class="p">):</span>
    <span class="k">pass</span>
<span class="n">warnings</span><span class="o">.</span><span class="n">warn</span> <span class="o">=</span> <span class="n">ignore_warn</span> <span class="c1">#ignore annoying warning (from sklearn and seaborn)</span>


<span class="kn">from</span> <span class="nn">scipy</span> <span class="k">import</span> <span class="n">stats</span>
<span class="kn">from</span> <span class="nn">scipy.stats</span> <span class="k">import</span> <span class="n">norm</span><span class="p">,</span> <span class="n">skew</span> <span class="c1">#for some statistics</span>


<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.float_format&#39;</span><span class="p">,</span> <span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">&#39;</span><span class="si">{:.3f}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">x</span><span class="p">))</span> <span class="c1">#Limiting floats output to 3 decimal points</span>


<span class="kn">from</span> <span class="nn">subprocess</span> <span class="k">import</span> <span class="n">check_output</span>
<span class="nb">print</span><span class="p">(</span><span class="n">check_output</span><span class="p">([</span><span class="s2">&quot;ls&quot;</span><span class="p">,</span> <span class="s2">&quot;input&quot;</span><span class="p">])</span><span class="o">.</span><span class="n">decode</span><span class="p">(</span><span class="s2">&quot;utf8&quot;</span><span class="p">))</span> <span class="c1">#check the files available in the directory</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>data_description.txt
sample_submission.csv
test.csv
train.csv
train1.csv

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#Now let&#39;s import and put the train and test datasets in  pandas dataframe</span>

<span class="n">train</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;input/train.csv&#39;</span><span class="p">)</span>
<span class="n">test</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s1">&#39;input/test.csv&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">##display the first five rows of the train dataset.</span>
<span class="n">train</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">5</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[3]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
      <th>SalePrice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>60</td>
      <td>RL</td>
      <td>65.000</td>
      <td>8450</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>208500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>20</td>
      <td>RL</td>
      <td>80.000</td>
      <td>9600</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>5</td>
      <td>2007</td>
      <td>WD</td>
      <td>Normal</td>
      <td>181500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>60</td>
      <td>RL</td>
      <td>68.000</td>
      <td>11250</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>223500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>70</td>
      <td>RL</td>
      <td>60.000</td>
      <td>9550</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>2</td>
      <td>2006</td>
      <td>WD</td>
      <td>Abnorml</td>
      <td>140000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>60</td>
      <td>RL</td>
      <td>84.000</td>
      <td>14260</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>2008</td>
      <td>WD</td>
      <td>Normal</td>
      <td>250000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 81 columns</p>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">##display the first five rows of the test dataset.</span>
<span class="n">test</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">5</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[4]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>MSSubClass</th>
      <th>MSZoning</th>
      <th>LotFrontage</th>
      <th>LotArea</th>
      <th>Street</th>
      <th>Alley</th>
      <th>LotShape</th>
      <th>LandContour</th>
      <th>Utilities</th>
      <th>...</th>
      <th>ScreenPorch</th>
      <th>PoolArea</th>
      <th>PoolQC</th>
      <th>Fence</th>
      <th>MiscFeature</th>
      <th>MiscVal</th>
      <th>MoSold</th>
      <th>YrSold</th>
      <th>SaleType</th>
      <th>SaleCondition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1461</td>
      <td>20</td>
      <td>RH</td>
      <td>80.000</td>
      <td>11622</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>Reg</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>120</td>
      <td>0</td>
      <td>NaN</td>
      <td>MnPrv</td>
      <td>NaN</td>
      <td>0</td>
      <td>6</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1462</td>
      <td>20</td>
      <td>RL</td>
      <td>81.000</td>
      <td>14267</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Gar2</td>
      <td>12500</td>
      <td>6</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1463</td>
      <td>60</td>
      <td>RL</td>
      <td>74.000</td>
      <td>13830</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>MnPrv</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1464</td>
      <td>60</td>
      <td>RL</td>
      <td>78.000</td>
      <td>9978</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>Lvl</td>
      <td>AllPub</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>6</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1465</td>
      <td>120</td>
      <td>RL</td>
      <td>43.000</td>
      <td>5005</td>
      <td>Pave</td>
      <td>NaN</td>
      <td>IR1</td>
      <td>HLS</td>
      <td>AllPub</td>
      <td>...</td>
      <td>144</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>1</td>
      <td>2010</td>
      <td>WD</td>
      <td>Normal</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 80 columns</p>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#check the numbers of samples and features</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;The train data size before dropping Id feature is : </span><span class="si">{}</span><span class="s2"> &quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;The test data size before dropping Id feature is : </span><span class="si">{}</span><span class="s2"> &quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">test</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>

<span class="c1">#Save the &#39;Id&#39; column</span>
<span class="n">train_ID</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s1">&#39;Id&#39;</span><span class="p">]</span>
<span class="n">test_ID</span> <span class="o">=</span> <span class="n">test</span><span class="p">[</span><span class="s1">&#39;Id&#39;</span><span class="p">]</span>

<span class="c1">#Now drop the  &#39;Id&#39; colum since it&#39;s unnecessary for  the prediction process.</span>
<span class="n">train</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s2">&quot;Id&quot;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
<span class="n">test</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s2">&quot;Id&quot;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>

<span class="c1">#check again the data size after dropping the &#39;Id&#39; variable</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">The train data size after dropping Id feature is : </span><span class="si">{}</span><span class="s2"> &quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span> 
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;The test data size after dropping Id feature is : </span><span class="si">{}</span><span class="s2"> &quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">test</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>The train data size before dropping Id feature is : (1460, 81) 
The test data size before dropping Id feature is : (1459, 80) 

The train data size after dropping Id feature is : (1460, 80) 
The test data size after dropping Id feature is : (1459, 79) 
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="&#25968;&#25454;&#39044;&#22788;&#29702;">&#25968;&#25454;&#39044;&#22788;&#29702;<a class="anchor-link" href="#&#25968;&#25454;&#39044;&#22788;&#29702;">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="&#24322;&#24120;&#20540;">&#24322;&#24120;&#20540;<a class="anchor-link" href="#&#24322;&#24120;&#20540;">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="http://ww2.amstat.org/publications/jse/v19n3/Decock/DataDocumentation.txt">Documentation</a>  Ames Housing数据文档中说明训练数据中存在异常值</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>让我们来探索一下这些异常值</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">()</span>
<span class="n">ax</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s1">&#39;GrLivArea&#39;</span><span class="p">],</span> <span class="n">y</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">13</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;GrLivArea&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">13</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们可以看到，在图的右下角有两个点，表明有面积很大的房子卖了很便宜的价格。这些值是很违反常识的。
因此，我们可以安全的删除他们</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#Deleting outliers</span>
<span class="n">train</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">train</span><span class="p">[(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;GrLivArea&#39;</span><span class="p">]</span><span class="o">&gt;</span><span class="mi">4000</span><span class="p">)</span> <span class="o">&amp;</span> <span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">]</span><span class="o">&lt;</span><span class="mi">300000</span><span class="p">)]</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>

<span class="c1">#Check the graphic again</span>
<span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">()</span>
<span class="n">ax</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;GrLivArea&#39;</span><span class="p">],</span> <span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">])</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">13</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;GrLivArea&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">13</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#27880;&#24847;&#65306;">&#27880;&#24847;&#65306;<a class="anchor-link" href="#&#27880;&#24847;&#65306;">&#182;</a></h3><p>删除异常值并不总是安全的。我们决定删除这两个值，因为它们值非常大且非常糟糕（价格非常低大面积房子）。</p>
<p>训练数据中可能还有其他异常值。 但是，如果测试数据中也存在异常值，则删除所有这些异常值可能会严重影响我们的模型。 这就是为什么我们有时候并不将它们全部删除，而是设法使我们的模型更加健壮。 你可以参考这个笔记本的建模部分。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="&#30446;&#26631;&#21464;&#37327;">&#30446;&#26631;&#21464;&#37327;<a class="anchor-link" href="#&#30446;&#26631;&#21464;&#37327;">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>SalePrice</strong> 是我们需要预测的变量。 所以我们先对这个变量做一些分析。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">sns</span><span class="o">.</span><span class="n">distplot</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">]</span> <span class="p">,</span> <span class="n">fit</span><span class="o">=</span><span class="n">norm</span><span class="p">);</span>

<span class="c1"># Get the fitted parameters used by the function</span>
<span class="p">(</span><span class="n">mu</span><span class="p">,</span> <span class="n">sigma</span><span class="p">)</span> <span class="o">=</span> <span class="n">norm</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span> <span class="s1">&#39;</span><span class="se">\n</span><span class="s1"> mu = </span><span class="si">{:.2f}</span><span class="s1"> and sigma = </span><span class="si">{:.2f}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">mu</span><span class="p">,</span> <span class="n">sigma</span><span class="p">))</span>

<span class="c1">#Now plot the distribution</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;Normal dist. ($\mu=$ </span><span class="si">{:.2f}</span><span class="s1"> and $\sigma=$ </span><span class="si">{:.2f}</span><span class="s1"> )&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">mu</span><span class="p">,</span> <span class="n">sigma</span><span class="p">)],</span>
            <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;best&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Frequency&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;SalePrice distribution&#39;</span><span class="p">)</span>

<span class="c1">#Get also the QQ-plot</span>
<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="n">res</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">probplot</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">],</span> <span class="n">plot</span><span class="o">=</span><span class="n">plt</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>
 mu = 180932.92 and sigma = 79467.79

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>目标变量是右倾斜的。 由于（线性）模型更适用于正态分布的数据，我们需要对此变量做转换以使其更像正态分布。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>对目标变量做对数变换</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#We use the numpy fuction log1p which  applies log(1+x) to all elements of the column</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">log1p</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">])</span>

<span class="c1">#Check the new distribution </span>
<span class="n">sns</span><span class="o">.</span><span class="n">distplot</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">]</span> <span class="p">,</span> <span class="n">fit</span><span class="o">=</span><span class="n">norm</span><span class="p">);</span>

<span class="c1"># Get the fitted parameters used by the function</span>
<span class="p">(</span><span class="n">mu</span><span class="p">,</span> <span class="n">sigma</span><span class="p">)</span> <span class="o">=</span> <span class="n">norm</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span> <span class="s1">&#39;</span><span class="se">\n</span><span class="s1"> mu = </span><span class="si">{:.2f}</span><span class="s1"> and sigma = </span><span class="si">{:.2f}</span><span class="se">\n</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">mu</span><span class="p">,</span> <span class="n">sigma</span><span class="p">))</span>

<span class="c1">#Now plot the distribution</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">([</span><span class="s1">&#39;Normal dist. ($\mu=$ </span><span class="si">{:.2f}</span><span class="s1"> and $\sigma=$ </span><span class="si">{:.2f}</span><span class="s1"> )&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">mu</span><span class="p">,</span> <span class="n">sigma</span><span class="p">)],</span>
            <span class="n">loc</span><span class="o">=</span><span class="s1">&#39;best&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Frequency&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;SalePrice distribution&#39;</span><span class="p">)</span>

<span class="c1">#Get also the QQ-plot</span>
<span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
<span class="n">res</span> <span class="o">=</span> <span class="n">stats</span><span class="o">.</span><span class="n">probplot</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">],</span> <span class="n">plot</span><span class="o">=</span><span class="n">plt</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>
 mu = 12.02 and sigma = 0.40

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>现在偏差被纠正了，数据看起来更正态分布。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="&#29305;&#24449;&#24037;&#31243;">&#29305;&#24449;&#24037;&#31243;<a class="anchor-link" href="#&#29305;&#24449;&#24037;&#31243;">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们先把训练数据和测试数据放到一个dataframe中。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">ntrain</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">ntest</span> <span class="o">=</span> <span class="n">test</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">y_train</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">SalePrice</span><span class="o">.</span><span class="n">values</span>
<span class="n">all_data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">((</span><span class="n">train</span><span class="p">,</span> <span class="n">test</span><span class="p">))</span><span class="o">.</span><span class="n">reset_index</span><span class="p">(</span><span class="n">drop</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">all_data</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;all_data size is : </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">all_data</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>all_data size is : (2917, 79)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#32570;&#22833;&#20540;">&#32570;&#22833;&#20540;<a class="anchor-link" href="#&#32570;&#22833;&#20540;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data_na</span> <span class="o">=</span> <span class="p">(</span><span class="n">all_data</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">all_data</span><span class="p">))</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">all_data_na</span> <span class="o">=</span> <span class="n">all_data_na</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">all_data_na</span><span class="p">[</span><span class="n">all_data_na</span> <span class="o">==</span> <span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">index</span><span class="p">)</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)[:</span><span class="mi">30</span><span class="p">]</span>
<span class="n">missing_data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s1">&#39;Missing Ratio&#39;</span> <span class="p">:</span><span class="n">all_data_na</span><span class="p">})</span>
<span class="n">missing_data</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">20</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[11]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Missing Ratio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PoolQC</th>
      <td>99.691</td>
    </tr>
    <tr>
      <th>MiscFeature</th>
      <td>96.400</td>
    </tr>
    <tr>
      <th>Alley</th>
      <td>93.212</td>
    </tr>
    <tr>
      <th>Fence</th>
      <td>80.425</td>
    </tr>
    <tr>
      <th>FireplaceQu</th>
      <td>48.680</td>
    </tr>
    <tr>
      <th>LotFrontage</th>
      <td>16.661</td>
    </tr>
    <tr>
      <th>GarageQual</th>
      <td>5.451</td>
    </tr>
    <tr>
      <th>GarageCond</th>
      <td>5.451</td>
    </tr>
    <tr>
      <th>GarageFinish</th>
      <td>5.451</td>
    </tr>
    <tr>
      <th>GarageYrBlt</th>
      <td>5.451</td>
    </tr>
    <tr>
      <th>GarageType</th>
      <td>5.382</td>
    </tr>
    <tr>
      <th>BsmtExposure</th>
      <td>2.811</td>
    </tr>
    <tr>
      <th>BsmtCond</th>
      <td>2.811</td>
    </tr>
    <tr>
      <th>BsmtQual</th>
      <td>2.777</td>
    </tr>
    <tr>
      <th>BsmtFinType2</th>
      <td>2.743</td>
    </tr>
    <tr>
      <th>BsmtFinType1</th>
      <td>2.708</td>
    </tr>
    <tr>
      <th>MasVnrType</th>
      <td>0.823</td>
    </tr>
    <tr>
      <th>MasVnrArea</th>
      <td>0.788</td>
    </tr>
    <tr>
      <th>MSZoning</th>
      <td>0.137</td>
    </tr>
    <tr>
      <th>BsmtFullBath</th>
      <td>0.069</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>将数据缺失的比例用直方图画出来：</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">f</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span> <span class="mi">12</span><span class="p">))</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xticks</span><span class="p">(</span><span class="n">rotation</span><span class="o">=</span><span class="s1">&#39;90&#39;</span><span class="p">)</span>
<span class="n">sns</span><span class="o">.</span><span class="n">barplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="n">all_data_na</span><span class="o">.</span><span class="n">index</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="n">all_data_na</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s1">&#39;Features&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">15</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s1">&#39;Percent of missing values&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">15</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s1">&#39;Percent missing data by feature&#39;</span><span class="p">,</span> <span class="n">fontsize</span><span class="o">=</span><span class="mi">15</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[12]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0.5,1,&#39;Percent missing data by feature&#39;)</pre>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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AABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgICIPAABgIJs3egAY2Wlv++WF7PfQe7/5B7a97e33W8ixkuTe9/qrH9j2F+++/8KO96B7nPID20587+KOd/Sdf/B4j//AYv7ujr/9D/7dAQCsJyt5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAAxF5AAAAA9m80QMAkBx1+hMXst/XHvK8Fbc/9AMvXsjxTr79MQvZLwAwP5EHwMI97P1/tpD9nnSHh698vH9842KOd8cHrrj94ae9dSHH+7ND77OQ/QIwNqdrAgAADETkAQAADETkAQAADETkAQAADETkAQAADETkAQAADETkAQAADETkAQAADETkAQAADETkAQDw/7d35vG6lXP/f5/TXEQaNCBKfSoUUU9oEE+RmdJgDKkMoeQpSaKEDGlCGmiQqYioTNGgwS8q8uiTNBijRKG5c35/fK919jr77FM9zvpe9+k+1/v1Oq+99r33Xp/7rPu+13V950ajMUY0I6/RaDQajUaj0Wg0xoiFR/0EGo1Go9Fo/N94wznfTznvcZttMcdjO53zkxQtgGM2e2bauRuNRmNBpkXyGo1Go9FoNBqNRmOMmC8jeZKmA58G1gPuBHayffVon1Wj0Wg0Go1Go9FozP/Mr5G8lwKL2346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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>数据相关性</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#Correlation map to see how features are correlated with SalePrice</span>
<span class="n">corrmat</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span>
<span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">12</span><span class="p">,</span><span class="mi">9</span><span class="p">))</span>
<span class="n">sns</span><span class="o">.</span><span class="n">heatmap</span><span class="p">(</span><span class="n">corrmat</span><span class="p">,</span> <span class="n">vmax</span><span class="o">=</span><span class="mf">0.9</span><span class="p">,</span> <span class="n">square</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[13]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x2a38d257198&gt;</pre>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAApkAAAJCCAYAAACLVty+AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzs3XmYVMXZ9/HvMAwzIOKCC+KGRr2VuESNBnfgcUui0RijJhqDxBhF3Ne4RJ+4RI1GY3w0cYsr0bhFTdQ3iWSMK+5iRG7cQEVFlkEWYdZ+/6hq7TQ9M9RhZmiY3+e6+pru03XXOX2mu6emqk7dFblcDhERERGRjtRjaR+AiIiIiCx/1MgUERERkQ6nRqaIiIiIdDg1MkVERESkw6mRKSIiIiIdTo1MEREREelwPZf2ASwvGme8m7wW1Cb23eT97L2iJcd8valXcszUymxLW63dXJEck2VXjem7YUrPluSYnrkMOwKmVTQmx0xunpsc00z6yfvjOg3JMQCPvz8wOaZ3S/rxTeuZfs6zvFs3bUj/HQGsWJke91TPPskxB646LTmmdvqayTEAU3umn8HN6tNjvDq9X6Ouojk5Zq2WyuQYyNbrkv6tAgszfK1UZVxtsE8Xfb9mOQ9ZYup6ZImCCyePyfZl3sGytBVSVK22YVm8zjz1ZIqIiIhIh1NPpoiIiEhXaEnvmV+WdUoj08yGAv8CDnH3uwu2jwdeBq4FLgQqCL2pj7j7FbHMmcDuhJ70HHCWu7/Uyn4GAXe5+5ASz+0PnBD30Rv4tbvfa2bnA5+4++875MWKiIiIyCI6sydzIvAD4G4AM9sCWCE+dw1wuLtPNLMq4BkzGwvUA98BdnL3nJl9DbgV2Cplx2a2I3AS8G13n2dm/YHnzGxCR7wwERERkWS5bHNKl1Wd2ch8DdjEzFZ299nAYcCdwHrAFGC0mf0ReJXQqGwws9Xi8yPN7DF3f9XMtgcws1rg6NgwPRoYANwCrG5mDwFrAH9z9wuAnwJXufs8AHefGeuZnT84M6sE/gCsC/QHHnX3c83sAOAMoBGYDBwO7ABcEbfVAYe6e/pVGiIiIiLdRGdf+HM/8F0zqwC2B56J238CTAOuAz4FrjCzanefQezJBJ41s4nAPu3soy/woxjzTTPbChgIvFtYyN3r3L3wqq51gefcfS9gZ+CYuP0HwJXuvjPwd6AfsH98LbsBNwOrJJ0FERERkZaWzr2Vmc5uZI4BDgF2BZ6M22qAbdz9AnffHtiE0Ht5lJltBMxx95Huvh6h9/M6M1u1qN7CS/Rfc/fP3L0ZeD7WN4XQiPyCme0U68+bBWxnZncCVwLVcfvJwK5m9gSwI2Fu6MWEntLHgQMJPZoiIiIi0opObWS6+7uEeZjHA3fEzS3AHWa2eSwzk9AorAe2JDQqa2LZScBnQDOwEFgrbt+mYDebmVlfM+sJfAN4A/gjcJqZrQBgZmvEbYWL1Y0AZrv7oYSh8D6xx/Uo4Hx3343QmP0ucChwi7sPi/UftYSnRkRERLqZXK6lU2/lpiuWMLob+JG7TzKzDYEG4CDgD7FhmANeAG529yYz2wwYZ2bzCI3g09z9MzO7Gvg/M/sAmFpQ/6y4j9WBu919AoCZXQ/8w8waCVeX/9zdx8c5lxB6Je8ys12A+cBbhGH252PcTGAu8FdgI+DWeEwNqJEpIiIi0qaKXK5TF5/vNpTxJ1DGn0AZfwJl/AmU8SdQxp9AGX+yxyzrGX8aPny9UxtdvdbZoixeZ54y/oiIiIhIh1PGHxEREZGuUIbzJjuTGpkdJMvQ9yR/IDlm3s9GJsd8Mj59qO6ehmyrNK3V2JQc83mP9KGttXL1yTEbZxgD+rCyuv1CJeyaIXPYYFuQHFOzbvpgxKP/Wqv9QiW0ZBiEGbblh8kx/xq/TnLMJxmG2Pv3WpgcAzC+ZcXkmO+tkj70/fDM9KHvgzb5IDkGYPbH6d8RLzb2T445dPWPk2N69Un/MD311trJMQB9M6T8m9wr/c/oOo3pI6YLemQbBV2tKf07+d0Mr6mrhuWP2Gpq+4WkbKiRKSIiItIVulnucs3JFBEREZEOp55MERERka6gOZkdz8yGEvKOH7IYZUe7+zVmNggYD7xc8PRYd//lEhzHesBW7v5w1jpEREREpH3l2JN5DnBNvD/B3Yd2YN3DgU0BNTJFRESka5VhfvHOtNQamWa2B3AhIV3kTGAkcCywqpldC1zWStxQ4FJC5p3rgU9K1PM14IxYZgNCRqBLgDMJ6SOfIaSrPC9W2wc4PGYlOpeQSnJ63H4u8ApwE5C/nPJ4d3+9I86DiIiIdA/lmPqxMy2VC39ijvDrgQNijvAngHPc/SJglruPikUHm1ltwS2/LkWNu+9CyIe+SD2xzPrA94AdgNPdvZnQ0Bzj7g8BXwUOc/fhwEPA981sK+CbwHbA/nyZK/0s4PGYu/wo4LrOOC8iIiIiy4ul1ZO5GjDH3fMLXv0buLhEuUWGy81sY8DbqeevwOvu3gQ0mZVcgHAqcHXMR7428DSwGfB8bJAuMLMXY9ktgOFmdnB8nG0RSREREem+utlw+dJawmgG0M/M8j2FuwGT4v3FWZ41/1tqq55SS8O28OVrvhE4wt1HAB/F/b4BbGdmPcysGtg6lp0IXBkbvAcBdy7GMYqIiIh0W13Zk7lnQc8gwK+A+82sBagDRsTtE8zsDr4c9m6Vu+fM7Kcl6tm8lZDXgbPN7GXgdmCcmdUB04CB7v66mT0CPEdowDbG20XATWZ2FNAPOH+xX7WIiIgIaAmjzuDutcCqJZ66vkTZYQUPh7RSV23B438C/ywqVlxmQPz5CmBx813AyYVBZrYGUOfu28eezDeAD9x9JmGOpoiIiIgshnJcwmhpmkEYLn+BMNx+o7u/v5SPSURERJYH3SytpBqZBdy9BTgiS+zeK1r7hYrM+9nI5Ji+f7g5OcY3b3fmwSJWqVqcqbGLmtyra95SPRp7JccMrFyYHLNqc1NyDMAbvdKPb40P+ybH9KlrSI6pr8j2u/08wwzuT99Of02rt2R4Tc3VyTGfNvdOjgH4PP1Xi3/Sv/1CRRrSXxLvefp+AFZfdX5yzNSq9P1M/rDUgFbbKktOr2/bwIr0zzrAlMqa5JgFGT5OsyrTg3qnnwYApvVM/07um2FEN8v3Q32Wc/dW+u8ISg+lSudTI1NERESkK3SzOZlL6+pyEREREVmOqSdTREREpCtonczyZmZDzeyuxSw7uujxGWb2sZllm9QhIiIiIotlmWtkJiq+4uVQwtJFhyyFYxEREZHuLNfSubcys1wMl5vZHsCFwEJgJjASOBZY1cyudfdRZjYUeAf4PSHn+S0xthaYTkgV+W3gWmBjQgP8HHevNbMDY335a+EOdPcZXfLiRERERJZBy3xPpplVEBZ1P8DddwOeIDQOLwJmufuoWPRIwrqXDtSb2TcKqhnj7rsTGqcz3H1XYD/g/+LzmwDfjmklHdirs1+XiIiILGdaWjr3VmaWh57M1YA57j41Pv43cHFhATNbBfgWsIaZHQesBIwGxsUiHn9uAexS0ADtaWb9gU+BW81sHrAp8GxnvRgRERGR5cHy0MicAfQzs7Xc/WNgN2BSfC4/vH0YcJO7nwZgZn2A98xs9fh8vvk/EfjQ3S82s97A2UAT8L/AerHMPwrqFREREVksuZwy/iwL9jSzFwse/wq438xagDpgRNw+wczuIPRQ/ihf2N0/N7P7gJ8W1fsH4AYzewLoR5ifOQd4GngZmB/rH9jhr0hERERkObLMNTLdvZbSGaKuL1F2WBv15OdqXlywrR44vETxg9KOUkRERKRIGV4B3pmW+Qt/RERERKT8LHM9meXq6029kmM+Gd8nOcY3L176s33f/s+FyTHnfP3s5BiA807slx5U35Ac0vDq5OSYD8etkBzz9+beyTEAPxn4UXLMyvuskxzTMr0uOWb4Ux8nxwDcNX2t5JhBp26YHPPO/6avDvZBVXIIB5yQ7Xe7yR1T2y9U5I3p/ZNjXqn4PDnmyD0+S44BaPk8fZ7Y6K9nOOmrrN5+mWJz5iaHTPlD+ucPYN2VZyfH/GZ6+mvavCX9T29VLpccA0BF+iUEn2RoGWzQkH58U6rSj23d+85MjikrZXgFeGdSI1NERESkK2i4XERERERkyagnU0RERKQrtGgJo05jZhsAlwP9gSrgNeAMd0+fdNP6PgYBd7n7EDObDGzq7gvN7IeE1JDNhB7c6939tgz11wJHu/vEjjpmERERkeVNlw2Xx8XNHwIuc/eh7r4TIePOn7pg3/sCPwG+FVNG7gEcbGbf7+x9i4iIiABhTmZn3spMV/Zkfht4wt3zqRxx91vN7Pi4iPqK7j7fzE4jZNm5l7D2ZQ2wEDgKqAQeBmYCjxAaqefF6voQ1rgsdanyccDp7v5Z3O8CMzuFsPj6PWb2ibsPADCzu4DfExZfvxFYmZC68gZ3v67DzoaIiIjIcqwrL/zZEHinxPZJwAvA9+LjQ4DbCMPqV8cF1S8HLonPDwD2dPfLgK8Ch7n7cEIvaWs9k+sD7xZtmwwMauN4NyIMu+8J7AOc3EZZERERkba1tHTurcx0ZU/mVGD7Ets3Bg4F/s/MJgKT3H2mmW0BnGVmZxByhed7KN9z9/z9qcDVZjYPWJuQ/rGUKYRG7ksF2zaJ8cXyC3d9ApxoZgcQUktmWBROREREpHvqykbmg8DZZra9uz8PYGZHAtPd3c2sAjgNyA9JTwQud/dnzGxTYLe4vbCpfiOwobvPNbNb+bKBWOwa4NLYYNyacAHQanE7QJWZ9SU0ZL8at50KPOvu15nZMMJwv4iIiEg2XTxv0sx6ANcCWwH1wJHu/nZ87mvAVQXFhwD7A88TRpn/E7c/4O6/zbL/Lmtkuvu8eAHOlWbWP+57PPCDWOQm4ALgX/HxqcB1ZlYD9AZOKFHt7cA4M6sDpgEDW9n3Q2a2AvAokIv1zQE2iEWuAp4jDKlPidsejvs/lDAHtMnMqrO8dhEREZGlYH+gxt13MLMhwBXAfgDu/iowFCBeCP2Ruz9mZrsDf3L345Z05126hJG7vwN8p5XnxgBjCh6/C+xVouiQgjInU3qu5JD4/KCCsn+i6Ep2M9sxPncBoYFbbNMS24aWOn4RERGRNnX9vMmdgccA3P05M/t6cYHYCfe/wK5x07bANmb2BPApcLy7Z8pH3K0z/rj7M0v7GEREREQ6ST/gs4LHzWZW3MH4E+Aed58RH08EznP33YC/AL/LunNl/OkgUytzyTH3NKySHLNKVWvTTlt3ztfPTo658MWLkmMAthh8cHLMBZWbJMc8Wb1GcsxaufRrt9ZrSg4B4KKPV0uOmX/D/OSYGmqSY7ZvWik5BiD93QoXXzozOaa6Ov1/3+0Wpv+ijrw2/XwDbMrqyTFrZPjcrluR/rv9bW3v5BiAPrn047v76VKLhbTNqtI/F70rKpNjtmxeNTkGYMGn6TFDGtK/++ekvySaW73koJ19ZehKWj/Da/qkZ/rxrZYh+c2Ve9+UHgScOWVYprgO1/U9mXOAFQse93D34i/MQ4EDCx6PBT6P9x8Afpl15926J1NERERkOfY08C2AOCfz9cInzWwloNrdPyjYfCNfLiv5P/z3yjxJ1JMpIiIi0gVyuS7PXf4AsIeZPUNYgecIMzsZeNvdHyIs5zi5KOZM4GYzGwXMB47MunM1MkVERESWQ+7eAhxdtHliwfMvEK5AL4x5D+iQ+QWd3sg0sw0IGXv6ExY0fw04w93nduA+BhGy8wwxs8nApu6+0Mz2Jyx9VEFYtujX7n7vEu7rixSUIiIiIoutDLPydKZOnZNpZr0J6R4vc/eh7r4TId/4n9qO7JB97wicBOzr7kMJcxJ+ZWaDO3vfIiIiIt1dZ/dkfht4wt3H5Te4+61mdryZtQAruvt8MzsNaALuBa4HaoCFwFFAJWFh9JnAI4RG6nmxuj7A4XyZcrLQT4Gr3H1e3O9MM9semG1mKwN3EC7t7wmc4+5jzWw88ASwJWHR9v2AefGYvkrIva4F2UVERCRdF2f8Wdo6++ryDQkNs2KTgBf48uqlQ4DbCMPqV7v7sHj/kvj8AGBPd7+M0Ng7zN2HE3pJv9/KvgcSMvh8wd3r3D0HnAP8w913jfE3xdRL/Qir3O9GyGv+zXircfchwM8JDVsRERERaUNnNzKnAoNKbN+Y0AN5eOxdnOTuM4EtgLPMrBb4BZBfDPE9d8/3Vk4FrjazWwgTU1tb/HAKsG7hBjPbycw2AjYD/g3g7lMJ60jlF797Jf78gNCj+lVCHk/c/f24XURERCRNS0vn3spMZzcyHyRcOr99foOZHQlMd3cnXJBzGnBDfHoi4aKgocDPCMPnAIVn7kbgCHcfAXwU6yjlj8BpMV0SZrZG3NYHeBPYJW5fm7DOdH7V6OJVaCcCO8SyA4G1F++li4iIiBTItXTurcx0aiMzzofcFzjHzJ42s3HAN4AfxCI3AdsA/4qPTwXOi/kybwPGl6j2dmCcmT1NWMV+YCv7fpYwl/Ifsb6/Aj939/HAxcBwM/s3IWXSUSVWwM/X8yDwQTz2q4AZpcqJiIiIyJc6fQkjd38H+E4rz40BxhQ8fhfYq0TRIQVlTgZObq2Muw8qKHsncGeJ/c6iaF2oErFnFtw/rdTxi4iIiCy2MhzS7kxKKykiIiIiHU4ZfzrI2s2tTQ1t3VqNJUfo2zS5V/qv7LwT+yXHbDH44OQYgNcn3J0c03jPlckxO93+n+SYubNqkmMA7l2wanLMQQuKp/a272vDZyXHzH4z/f3wyMw1k2MAnunxeXLMiU3p/7XncumfpcdrVkiO2ZKeHPvdz5Ljpj5SlxwzpmGV5JiPqE+O+W59thXWVs6VWgWubcc9cUFyTNN9NyXH5OrSf0fQwOT709P3Lahv7TrS1v2w6f3kmDMrN0uOmVKV/p0C0K8l/fP0Xq/0mJUzdNDVVabHVOfgZ2esnB5YLspw3mRnUk+mSBuyNDBl2ZClgSnLhiwNTFk2LNMNzG5IPZkiIiIiXUFzMkVERERElkxZ92Sa2b3Ai+5+SXzcF3gJOMjdX8tQ3yDCskgvE9bX7AOc6O5PtxFzv7sfEBeIPxr4FNg7XhkvIiIisnjUk1lWjgaOMbPB8fHlwPVZGpgFJrj70Jg68lDgD20VdvcDijZtSStLMomIiIhIUNY9me4+w8xGAzea2c+BrxAanVsAVxN6I2cCI4F5hAbjukB/4FF3Pzemn+wfb8cW7WIVYDJALHeXuz9mZnsDh7j7CDP7xN0HFMScDWxlZke5+/Wd8bpFRERkOaSry8uLuz9MSO14CzDC3XOENJTHxvSTjwCnExqXz7n7XsDOwDEF1Yx19x2BOmCwmdWa2VPAWOBPiYd0UaxPDUwRERGRVpR1T2aB24A+7j41Pt4MuNbMAKqAScAsYDszGwbMAQoXjPOC+xNi4xQzGwC8EhuchdIXCRMRERFpi+ZkLhMcODw2Fk8H/gaMAGa7+6HAFUAfM8s3Flv7rc4CFhAa2wuBteL2bdrYdwvL7nkTERER6RLLSk9msWOA28wsny/gJ8CbwF1mtgswH3gLGFgidnC8UrwFWAG4wd3fMbMbgZvN7FBCz2hr3gG2MLMT3f2qjnk5IiIistzrZnMyl4lGprvXArUFj18ChpYoukWJbSMK4iYDJXMsuvuLhCvHi7cPiD8L95eeE0xERESkG1kmGpkiIiIiyzzNyRQRERERWTLqyewglbn0mM97VLZfqCPUNySHXFC5SaZdNd5zZXJM1fdPSo55/4JTk2PmNPdKjqnvnRwCQO/K5uSYuW+n/8+3YH5Vcow1NCbHAHxak34yVl9jWnLMm1NXS46pzvBRys2vTw8CPpvXNzmmd1X6ghU1Fenvh7UrFyTHAHzaVJMc0/LSP5NjmiZNbb9QccyspuSYxqaVk2MAelenfza267leckxV+kuisgsXPemd4e9ZRYaYlbN06tVn+9yWjW42J1M9mSIiIiLS4dSTKSIiItIVutmcTDUyRURERLqCGpn/zczuBV5090vi477AS8BB7v5a6g7NbBAwHng5bqoh5B3/vrvXpdaXsN8v8pHHxwOBt4Efu/s9JcrXABPdfVDR9qOBAe5+fmcdq4iIiMiybnHmZB4NHGNmg+Pjy4HrszQwC0xw96HxNgR4gbCgelc6AvgtcGwX71dERES6o1yuc29lpt2eTHefYWajgRvN7OfAVwiNzi2Aqwl5vmcCIwk9kn8A1gX6A4+6+7lmdkt83J+iRl1M/bguoVcRMzsO+CGQA+5y96tjfCOwPiEn+V3AvsB6wH4xY88VwM6x2jHu/lsz2wy4mZABaD5QV7DPHwG7AA+a2ebu/p/YS3snsEr+eGL5nQkN0llAM/Bce+dNREREpDtbrKvL3f1hYCJwCzDC3XPADcCxMRPOI4Qc4usCz7n7XoQG3zEF1Yx19x0JDb3BZlZrZuMJKRzfBm6NvaUHx9idgf3NzGL8ZHffk5A+cgN3/xZwH7Cvme0DbAAMiXE/jI3gC4BfuPvuwDMFx/I/wOvuPp3QCM03fEcA/3H3XQmN5bwrgR+4+x7Ae4tzzkRERET+S0tL597KTMoSRrcB49w9v9DZZsC1MQ/4SEKe8FnAdmZ2J6FhVl0Q7wX3J8TG6TeAKcA0d28CNif0Vj4OjCX0fG4UY/JzOGcDE+L9OsKczs2AJ9095+6NhJ7GwcBXgedj2acL9v9TYAMze4zQa3qwma1UWN7dxxF6TwHWdvdJJeoRERERkRKWZJ1MBw6PjcXTgb8RegJnu/uhwBVAnzg0DbBIE9vdFwCHAr8ws61inW8Aw2K9twCvx+JtTTZ4kzhUbmZVwI7AW4Te1x1ime3i86sRejy/4e57u/twQo/ojwvLm9nWQH6l60/i0PsX9YiIiIgk6WY9mUuyhNExwG1mls+18RNCY+8uM9uFMAfyLUIPZ6vcfZqZnUoYnt6R0Iv5lJlVE3oV200R4e5/NbOhZvYs0Av4s7u/bGajgLvN7DRgOrAQOBy4z90LU7LcQOip3QK42cyeIjQ486kFDiMM588F5hLndoqIiIhIaYvdyHT3WqC24PFLwNASRbcosW1EQdxkQk9iYd13Ei64Afh1vLUWf2bB/asK7i+SZ9DdPwZ2LXE8xeWeBzaND39U4vkJwPbt1SMiIiLSKqWVFBERERFZMsr400EaK9ovU2ytXH37hYr0aOyVHNPw6uTkmCer10iOAdjp9v8kx7x/wSKd0O3advzlyTHv7Dg6OYaGVdJjgJnN6b+nDfo1JcdU9W5uv1CRWXP7JMcAtFSkf130Xbux/UJF5n5c2X6hIv0ydA7MyLgQWVVl+jnfvD49pqK6uv1CRfqv+llyDMCK9enfRe9f8GJyzGpfSX+PZzGvoar9QiXMbkj/bAyoSV+bcEGGvxfrN2ZbA/Gjnuk7a85wfD0yxCzM0M3V9OaU9KByUobzJjuTejJFREREpMOpJ1NERESkK5RhVp7OpJ5MEREREelwndrIjMsK5czs4KLt42OqyMWt5zYzG1m07SQzuzDxeB4ys4dTYkREREQ6RDdbJ7MrejInAj/IP4jpHldIrON6wvqWhX4M3Li4FZjZukBfYBUz2zBx/yIiIiKSoCvmZL4GbGJmK7v7bMLC5ncC65nZaOAAQmadz+L9QYRMP41AEyGr0FNmtrqZre/uU8xsO+ATd58ce0TrY9xahNzqL5vZFEID9013P5GwWPyDwAJgFHAqQGE5Qpai6wmpKhcCR7n7B2b2K+DrwIqxviM67WyJiIjI8qkMexs7U1fNybwf+G5MMbk98Ezcd39gd3ffhdDQ3A7YA3gJ2B24CMivIXMToYEKcAQhQ1DeFHffC/gdcFTcti7wQ3c/0cx6EHKU3w7cRchV3ru4HHA5cLW7D4v3LzGzfkCdu+9ByEg0xMzW7qDzIiIiIrJc6qqry8cA1wHvAk/GbS1AA/AnM5sHrENoaN4EnAE8RujdPCuWvw143MyuIGQaOr6g/lfizw+AneL9Ge4+M97fi9ALOSY+zjc6byoqtwVwlpmdAVTE41sArGFmfwLmEYbcsy3CJiIiIt2XMv50PHd/lzAP83jgjri5H7C/ux8MHBePpQLYD3jS3f8HuIfQ4MTdZxCGtM8FHnD3wlV9S60JUPibPBI40t33dve9gYOAY0uUmwic4e5DgZ8B9wLfBNZ19x8QGry943GKiIiISCu6cp3Mu4EfufukeOFNEzDfzF4kzKn8GBgIPAfcYWZNhAbgSQV13AA8Atji7tTM1gC+AXxxhbu7P21mNWa2Y1HxU4HrzKyG0Jg8AXgPONfMnovH+W48zvcW+5WLiIhIt5dr6V7rZHZqI9Pda4HaeP93hDmTuPtjhOHw1uzQSn2PA9VF20YU3P+iXncfEH9+ShiKL65rcLw7oGDbu4Sh9WLbtXGsIiIiIlJEGX9EREREukI3u7pcjcwOMqVn+htn48b0qZ0DKxcmx3w4LnVZUlgrl+3aprmzapJj5jT3So55Z8fRyTFfeeaa5Jjqbc9NjgH4Tt2T7RcqUrfFNskxzR/PS4656f3kEADWyzDK89rzaybH7PO7xZ4N84W/nuDJMU/NWiM5BqCuMj1mck1T+4WK9CH9O+Wx2dle0/Des5JjPq7rmxzTPDH9MoDefRuSY/r2akyOAfiksbr9QkV6ZPg9ZfnD2yPjKOua6W89Zmd4j2c5vOoMQc2z098PZUUX/oiIiIiILBn1ZIqIiIh0hW524Y96MkVERESkw3V6T6aZDQX+DEwgrC9ZBYx094kZ6xvt7teY2SBgPPBywdNjgYeA77j7L9uo40xCRqEWwlSSs9z9JTM7n7BI+0cFxU939+dj3InAAHc/M8uxi4iISDemC386xVh3PwTAzPYkpGzcJ2Nd5wD5KzgmxIXTi73aWrCZDQa+A+zk7jkz+xpwK7BVLPIbd/99UUxvwhqd3wDuy3jcIiIiIt3G0piTuQow2cxGAT8m9CY+5e6nmdktQCOwPmE9zLuAfYH1CJmADgFWNbNrgctKVR57To9290PM7C3gacLi7dOA7wGfxvpGmtlj7v6qmW3fzjHXENKivZY1AAAgAElEQVRa/hPYNOsLFxERkW6sm/VkdtWczOFmVmtmzwI3E9I1HgGc4O47AO+aWb7BO9nd9ySkkNzA3b9F6D3c190vAma5+6hYdnCsN39bu2i/GwLnxn2sDmwX01N+h5Dj/Fkzm8h/96qeXFBffvH4Onf/ewefExEREZHl1tIYLjfgWWA34BQzuzQ+zi8amZ9jOZuQSxygjtCbWGyR4XIz27jg4Qx3/yDe/wCoMbONgDnuPjKW/zrwiJn9K5ZbZLhcREREZInldHV5Z5sWf44mDGvvBmwN5POIt/cbSFnBvFRdW/JlfnKAScBnQHNCvSIiIiLShq7qyRxuZrWEhtyKwMlx3y+Y2XRgKjCOMITenglmdgfhAqBk7n6/mW0GjDOzeYSG9mnu/lnoZBURERHpBN1sTmanNzLdvRZoLdfZjUWPRxTEnVlw/6qC+8MKyg9pZX+18f6Agu2HFNy/CLioROz5rRxn/vlb2npeRERERAJl/BERERHpCt0s448amR2kZy5lqmjwYWV1csyqzU3JMX9v7p0cs176bgC4d8GqyTH16YcHDaskh1Rve25yzOkvXZAcA/Dqticlxzz5p/QT0VzRNzlmtVKX0C2GAS3p7/HXq3slx1QdPz45pqUi/bM0qSrbsFW/XPpU9vVa0r9qF6afbuZknGX//Pz0z+2bvdPP30pN6Z/bqrrkENZpzPaHfHrP9JP+1cbKDPtJDmGVpmyvqb5HhjdSBk0ZdtMnw0fwzufWSQ8iXAQiXU+NTBEREZGukOteczKVu1xEREREOpx6MkVERES6guZkdqyY5vHPwATCGpdVwEh3n9hWXBv1jXb3a8xsEDCeLxdvBxgLPAR8x91/2UYdZwK7E1Ja5oCz3P0lMzsf+CHwUUHx04FPCJmKesbXcJS7e5bjFxEREekOlkbGnz2By/nvVI4pzgGuifcXyfgTvdpasJkNJqaVdPecmX0NuBXYKhZZJOOPmd0KXOPufzGzvYBfAQdkPH4RERHphnJaJ7PTrQJMNrNRwI8JvYlPuftpZnYL0AisD1QDdwH7AusB+wGHAKua2bXAZaUqjz2nR7v7IWb2FvA0YIRMQ98DPo31jTSzx9z9VTPbvp1jPoWQFQjCOVuY5YWLiIiIdBdddeHPcDOrNbNnCcPO9xKy+5zg7jsA75pZvsE72d33BN4ENnD3bwH3AfvGRdRnufuoWHZwrDd/W7tovxsC58Z9rA5s5+4ziD2ZwLNmNpH/7lU9uaC+3wG4+wx3b4x51y8H/rdDz46IiIgs/1pynXsrM0tjuNyAZ4HdgFPM7NL4OL/KVn6O5WwgP2+zDii1ut8iw+VmtnHBwxnu/kG8/wFQY2YbAXPcfWQs/3XgETP7Vyy3yHB5LDcMuBb4keZjioiISDItYdTppsWfownD2rsBWwM7xu3tNcVTlnwtVdeWwHVmlm+0TiIMhTe3VklsYP4W2NvdX0zYv4iIiEi31FU9mcPNrJbQkFsRODnu+wUzmw5MBcYRhtDbM8HM7iBcAJTM3e83s82AcWY2j9DQPs3dPwudrCVdBfQCbo1l3N1/lmX/IiIi0k2V4ZB2Z6rI5brXC+4s569/aPKJ3KgxPQ9XlrSSL9akpz1bL0uOMGBqz/T3U33XZD2jOsNbPWtayR9mSCt5xMIsaSXTT96TGdNKbtic/j7K8rvdpiH9urqPMqSVfD3LG4JsaSWrMuwqS1rJrB+lgRnSyL6ZIS3nSl107royreQKGUY/s6SV3Kg+2zDrvMr0c54lPWmGP2f0y/CSFmR8k4/+4I4u+kvTtvm/TG8rpFjhF3eWxevM02LsIiIiIl2hmy1hpLSSIiIiItLh1JPZQaZVNCbH7NrqpUate6NXr+SYnwz8qP1CRS76eLXkGICDFqSPBPSuTD8RM5vTz8N36p5Mjnk1w7A3wJiXrkyOWXD2MekxXp8cM+WddZJjINuw5bAVZibHDJ/7fnLMoSttmRxz7KrTk2MAxswckByzU4YpABN7ps9r2GXFGckxAM9/lv55/17T58kxvXqmf9brm9L/TD1TtUJyDMDg+vTv8Ym9qpJjVsrw3T+lV7Y+oSxTVjLMeqJ/htf0SYYWyD49Pmu/UDnrZnMy1ZMpIiIiIh1OPZkiIiIiXaGL18k0sx6ENb63AuqBI9397YLnryYkp5kbN+0HVAFjgN7AR8AR7p4+dIF6MkVERESWV/sDNTHz4ZnAFUXPbwPs5e5D4+0z4BfAGHffBXgFyLxkY5f3ZMbc4n8GJhBW3KgCRrr7xLbi2qhvtLtfU5izvOC5S4CJ7n5LK7EbAA8ArwGnAr8H+sbjmgIc7+4LzGwy8D4hzzqE1JYHZDleERER6aa6fk7mzsBjAO7+XMxyCHzRy7kxcL2ZrQnc5O43x5iLY7FH4/30Cw1Yej2ZY2OLeTfgfEI+8KwyLcoe7QQ87u4/Bk4D/uHue8Xc6fOBowvK7lnQ0lcDU0RERMpdP0JWw7xmM8t3MK4A/A44DNgbGGVmWxbFzAVWyrrzcpiTuQow2cxGAT8m9BY+5e6nmdktQCOwPlAN3AXsC6xHmDdwCLCqmV1L6B0tKfZyngE0ABsAdwO3ExqofczsbULP5YHx/tOEns3udRmYiIiIdJpc16+TOYeQaTGvh7vn0y98Dvw2P9/SzMYS5m7mYxbEn7Oz7nxp9WQON7NaM3sWuBm4l5BS8oQ4b+Ddgpb25Niz+Cawgbt/C7gP2NfdLyIMXY9qY1/5huL6wPeAHYDT3f194BLCvIPrgOsIE11PI0x0fQAYWFDP3+Mx15rZt5f4DIiIiIh0rqeBbwGY2RDg9YLnNgGeMrNKM6siDJO/XBgDfBNIX/8vWlo9mWPzcyctJAN/FtgNOMXMLo2P86t7vRx/zgby8zbrgOJF5BYQejsL9Y3bAV6PrfcmM1vAooYBt7n7zWZWDZxOyFn+vfj8nu6evtidiIiICCyNOZkPAHuY2TOEdtURZnYy8La7P2RmdwLPEUaNb3P3N8zsQuBWM/spMAP4Ydadl8Nw+bT4czThwp2FZvb/gB3j9vZ+I/nG6JvA1ma2lrt/bGY1wK6EhuI6i1HPCcCGwA3uXm9mbwCbJb4WERERkbLg7i389/Ul8GWHHe5+GXBZUcw0whzNJba0GpnDzawWaCaM958cj+UFM5sOTAXGEYbQ2zPBzO5w98Ni6/xvZvY50Av4nbu/bWaLk+LkaODaODd0ATAdSE/BIiIiIlJKN8v40+WNTHevBdZo5ekbix6PKIg7s+D+VQX3hxXcvx+4v5V91hY8HhB/3lKw7SPCelKljnlQK8crIiIiIiWUw3C5iIiIyPKvizP+LG1qZHaQyc1z2y9UZHDJ64/atsaHfZNjVt5ncWYL/Lf5N8xPjgH42vBZyTFz305f5GCDfk3tFypSt8U2yTFP/ql3cgzAgrPTZ1r0vui65Jjqj95Kjnli32uTYwC2/a9VMBbPmtvWJ8c8N2lAcsyDn1Qmx1T3TX8PAdTPTB/ueq9H8XWK7ZvSM30/QyuzDcXtvtGHyTEVGdYm6TM4/fNUUVPRfqEifR9O/x4CaOyR/j76B+nfyYMb0/ezZkO2xkldZfovalb64dGU/muiJsPbdaOL07/HZelRI1NERESkK2hOpoiIiIh0tFw3a2QurcXYRURERGQ51uE9mWZ2BbAtMADoA7wLTHf375coOwjY3N3/2kpdGwG3uPvOZvYUUEVYXqgP8Ki7n7cEx7kVsKK7P2VmmxDW0+xJaHg/D5wNVBJymD9bEPq6ux+Xdb8iIiLSTXWznswOb2S6+ykAZjYC2LRw6aESdgcGASUbmSUcGte97AE8Y2YPuPurGQ/1+8Bk4ClCesnfuPs/zawCeBDYB3iU0EAemnEfIiIiIt1Sl83JNLOrCHnDAW4HrifkCa+JOcwXAOfE53sDh7VRXTWhl/FjM1sTuDtu7wkcBTQAtwEfE3KWjyEkfd8a+AthPc4fAQvN7BVgCjAyLuL+AiGVZFPch4iIiMiSa9ESRh3OzPYHBgJDCEPezwBjgV8Dg9z9b2Z2HPADd59mZr8ADgTuK6rqzph3fENCTvNZhCTuMwiN0i2AlQjZer5CSIvUD3BCasl64B13/4WZ3Q5MdveXzOw/wLHApcDmwMPAcYSh8tVjdqK8E5eg91RERESkW+iqnszNgCfdPQc0mNk4Fs0LPhX4PzObR2gQ1paop3C4/DbgFEJD9SvAQ4QezAti2bfdfY6ZtQAfu3sdQBwOLzbU3X8D/MbM+gJXAmcR5mVquFxERESWXDebk9lVV5e/CewMYGa9CMPmbwEtBcdwPfBjdx8BTANaXdo1JnyfSshPPgz4wN33JPREXhiLtfebLNz3b8xsWKx7Xjy29FWkRURERAToup7MB4HdzOwZwnzKMe4+PjY4z4jzIscAL5hZHfApYXi92J1x3mQFMI8wr7IncLeZnURoOJ6/mMf0InCJmU0EDgJ+a2a/BhqBt4H0lC0iIiIirelmPZmd1sh091sK7ueAk0qUeRGw+PCeVqraOZbduY3dDW8jbh6wUcE+B8SfDxGG2PN2b6Xu9JyMIiIiIt2cMv6IiIiIdIFcTj2ZkkFzu1NAF1WzbvqU2D51DckxLdPrkmNqqEmOAZj9ZvpbasH8quSYqt7NyTHNH89Lj6nomxwDsMDTp/RWf/RWckyPgRsnxzTk0s8dhHkuqaoGpw8EzH1uZoY9pevVP9uX/afvNybH7NTc6hTzVlXXp3+W+n8j/fsBgB7px/fR832SY/psmu2911UWNKR/F/WpSv8er8rw1kv/DQU1mRo16XvL8poyWbigi3YkHUGNTBEREZGu0M3mZCp3uYiIiIh0OPVkioiIiHSFbtaTucw0Ms3sG8ClrS2MbmbrAVu5+8Nmdj7wQ+CjgiKnA6OAu9z9saLY7Qnra1YQencfcfcrzGwQMJ6QXShvrLv/skNelIiIiMhyaploZJrZ6YQ1Mee3UWw4sCkhJSTAb9z990X1jGol9hrgcHefaGZVwDNmNhaoAyYo44+IiIgsqZx6MsvSO8ABwO3wRWPxx4TF158Czoy3PnHB9zaZ2QhgJKHX8jxgCjDazP4IvArs5O4NsSdTRERERBItExf+uPt9hEw8eUcAJ7j7DsC7hGHuSwiZhPILrJ9sZrXx9rsS1da5+87u/jjwE0Iqy+sI2YauMLP8ii2DC+qpNbO1O+ElioiIyPKuJde5tzKzrPRkFjsCONXMLgWepfSiXosMlxdxADOrAbZx9wuAC8ysP3AzcBRh6F3D5SIiIiKJlomezBJ+Chzt7rsBWwM7EobOU15PS8HPO8xscwB3n0kYPk9fTVtERESkNS2dfCszy2pP5uvAC2Y2HZgKjAPmAGeb2cttRhaJcy8PAv5gZj2BHPACoTdTectFRESkQ+jCnzLl7pOBIfH+jcCNRUVeAaydOka0sv0ZYKcST32xTxERERFZfMtMI1NERERkmaaeTMnij+s0JMc8+q+1kmPqK0pd49S24U99nByzfdNKyTEAj8xcMznGGhrbL1Rk1tw+yTE3vZ8cwmo16TEAU95Jn2nxxL7XJsc05JqTY+59+erkGIB7tzw3OabH17ZJjrm0+cnkmC3SPxZU9sv29XfFOem/25b3PkiO+csf019U9Z7bJscAvHHe28kx7zSvkBwz96EFyTFzmquSY+ZXVCbHAKxX1dZSzKVZ+tcXUzO89VZrznYJxQoZGjUrZGgHZWk6pX97weybXsgQBb2PyBQmS0iNTBEREZGuUIYX53SmZfXqchEREREpY+rJFBEREekCurq8DMT84TcDg4Bq4MKCTD5txT0HHBLj/gxMKHh6DNAAbOruZxbFrQ78HuhLWNh9CnC8uy8ws8nA+3zZyT3L3Q/I+NJEREREuoWybGQChwEz3f1HMQPPK0C7jcwiY939kMINMWd5KacB/8hnCDKzq4CjgSvj83u6+8LE/YuIiIh8qZvNySzXRuY9wL0Fj5vMrBZ4Fdgc6Ad8392nmNlFwN7AB8Bqi1O5mQ0ipIycCTxC6Lk80MzeBp4GTiXbxXIiIiIiQpk2Mt19HoCZrUhobJ5DyCX+vLufGBuWPzCzvwK7AtsRhrrfKqhmeGyY5v1P0W4GANvGjD89gAWEHs17gKeAUYSGK8DfzSz//8ev3f1vHfNKRUREpLvQnMwyYWbrAg8A17r7GDM7ijBsDqHxNwD4KvCiu7cAc8zs9YIqSg2XFz58z93zi1sOA25z95vNrBo4HbgK+F58XsPlIiIiIgnKcgkjM1sT+DtwhrvfXPBU8b8ADmxvZj3MbAVgcMJuCmdGnAAcAeDu9cAbQH3ygYuIiIi0pqWTb2WmXHsyzwJWAc41s3yakd7Fhdz9VTO7B3gB+Aj4NOP+jgauNbNRhGHz6cAxGesSERER6fbKspHp7icQehdbe/73BfevIgxtF5oM1JaIu6Xg4ZCC7R8B+7eyr0HtH7GIiIhI23Jl2NvYmcpyuFxERERElm0VuVz3utKps9y29mHJJzLLPzSfZ/i3YF6GmFWa02MAnqj8PDlmo0VnQrSrpSI5hB4Z3+oDMuysKsO+plemx1Rn2M+Apmwn4sDxFyTHPPnVM9svVOTZmqrkmL65DG8Isr0n6jPsarP69A/UlF7pb4iNGxqTYwDGV6ef88YM56GuIv08VGfsC+mX4XO7YoYv5b4ZYmZl+KzXZPz+6pvhauYZlennriHD+6E528c209/OM6fckXFvHWvmt3fr1EZX/789URavM089mSJtyNLAlGVD1n86pPxlaWDKsqGbjTYv88pyTqaIiIjI8kZzMkVERERElpB6MkVERES6QjfryczUyDSzocDRxRl1MtTTF/gV8A3C+pRzgFPcfVJiPYOAu9x9iJndAmwDzCoocjhwMvAbd3+/lTo2An5LOCc9gReBn7t7i5k1AM8UFJ/g7qNSjlFERESkO1naPZm3Av9y9+MAzGwr4C9mtoO7f7YE9Z7u7o8VbTuxnZiLgd+5+2NmVgHcD+xHSG05y92HLsHxiIiISDfX3eZkdlgj08z2AC4EFgIzgZHALcCF7v6imTlwprs/YGZ/J6Rx3Njd8/nBcffXzOwh4AAzywGbuvuZZlYDTHT3QWa2G3BeDOlD6KXM5yBv6/hqCZl9DgE2ANYA1gdOcvf/B0wBRpjZXOB54CCgaYlOioiIiEjU3RqZHXLhT+z5ux44wN13A54AziH0Bn7TzDYgND73MLOVgBpgPeC9EtVNBga1sbuvAoe5+3DgIeD7JcpcZma18XZ2iefr3f2bhKxCJ8Vt5wDPEYbvPwX+CKwUn1u1oL5aM9u2jeMTERER6fY6qidzNWCOu0+Nj/9NGH6+CHgQmAFcSpgX+U3gYeB9Qo9isU2AiUXbChc9mwpcbWbzgLWBp0vUUWq4vNAr8ecHhAYvwLB8iso4V/Ry4FzgFDRcLiIiIktIPZnZzAD6mdla8fFuwCR3rwM+Bw4GHiM0LE8E7o8N0rfN7FgAM7vEzH5NmAd5D6HnM1/fNgX7uhE4wt1HAB/x3w3QxVVqGebL4pA/7j4PmATUZ6hbREREpNtbkp7MPc3sxYLHvwLuN7MWoA4YEbc/SGgUzjKz/weMcvd34nOHA78ys3GEC/s/J/QubkFolB5jZk8BLxGuPAe4HRhnZnXANGDgEryGQgcTekh/RZjj+S5wTAfVLSIiIt1dxhS4y6qyy10e52yu4+5vLO1jSaHc5cHylrs8a1pJ5S4Pyjl3eda0kspdHpRz7vKsaSWVuzwo59zlWUebyyV3+bShQzu10bVmbW1ZvM68pb2E0SLi0kVLsnyRiIiISNnpbnMyy66RuazqneG/xWFbfpgc8+nbfZNjBp26YXLMxZfOTI4BOLEp/RO0+hrTkmP6rp3eY/Pa82smx7xe3Ss5BmDYCunnb81t06cAVw1eJzmmx9e2ab9QCVl6JXd545LkmElb/yI5Zn6G/91H/Wr99CCg4R/PJcf03GTt5Jjaq9Pf47s+eVxyDMCQqy9Ojvng0fSTvt5+6V14uYb0leQ++me2zqIVVkr/DP71o/QZW1l6JQc2Zhteqih5CULbZlSmNw0GZFjw74P0DnROuHnX9CBZatTIFBEREekCuYxTOZZVHXV1uYiIiIjIF9STKSIiItIFNCdzKTKzDYHLgHUIyxktICys/kZBmUHAXe4+pCj2KuA37v5+G/VfBwxx96074fBFREREJCqbRqaZ9SGkifypuz8bt20P/B8wtL14dz9xMerfCfiPmQ1199olPWYRERGRxZXrZutklk0jE9gXGJtvYAK4+/NmNszMbgH6x9uxpYLNrBY4GrgDONDdJ5vZ94Gd3f0E4CDgceBRYDRQG+P+w5fZfY4Gbor7ATje3V83s9HAAUAVYXmlA9y9oeNeuoiIiMjypZwu/NkAeDv/wMwejA3HiYTh87HuviMhm1BbbiJkEoKQdeiGeP9IQkrKfwJbm1l+TZG+wAXu/gPgLOBxdx8GHAVcZ2Y9CI3O3d19F0JDc7sleJ0iIiLSDeVaOvdWbsqpkfkBoaEJgLvv5+5DCY3KDwFfzHruBA40s4FAP3f/j5ltBmwOXAE8QshdfnRBTL7uLYCRsXF7A7CKu7cQ0kz+ycxuIjR4M6zuJSIiItJ9lFMj80FgdzP74oIeM9uI0Khbn8XMJuXucwi5zq8E/hg3Hwmc7e57u/vewHBCYzK/0na+7onAlbFxexBwp5ltCezv7gcDxxHOWfeaVCEiIiJLLNdS0am3clM2czLdfZ6Z7QtcYmZrEY6tiTBsfVBR8c3N7MWCx6cUPX8D8BhfNiQPAbYq2Nf7ZvYacGBR3EXATWZ2FNAPOJ8whD8/7q8e+BhIT/EgIiIi0o2UTSMTwN0nExqExR4pKlMqt+LQgjLPEBqJeYvkdHP3b8W7Ywq2zQT2L1H38NaPWkRERKR9uWwZT5dZ5TRcLiIiIiLLiYpcd2tWd5Jr1j0s+USu2ZR+7ldvSV85aW5Feof1q9XZ/v/Yu+nz5JiZTdXJMXN7VCbH7PNbS4558fjxyTEAh9S/mRzz3EYDkmPmzqpJjrm0OT0GYJNcelz/DHOEfvLKL5NjRn/9jOSYNenVfqES+mRY5+6divrkmA1z6Z+LerJ9n++0sCk5pjnD1PTKDMe3Qo/0Y+tRke08vEOf5JjJVen7WinD56I645/qLHGfpn+9ZrJuY/rBbdm3vQVmStvsrUfKYsLilG1279RG1/ov/7MsXmdeWQ2Xi4iIiCyvyvHinM6k4XIRERER6XDqyRQRERHpAt1thmKHNjLNbCjwZ2ACYS3JKmCku0/MWN9od7/GzAYB44GXC54e6+4lJ2/FNJR3AQOATd39TDNrAJ6Jx9UXuNDdH2hj37sCs919vJl94u7pE+ZEREREuqnO6Mkc6+6HAJjZnsDlwD4Z6zoHuCbenxAXSc9qVj7ezFYCJpnZX9y9tf8rRhIaqtmu/BAREREp0N3mZHb2cPkqwGQzGwX8mJBZ5yl3Py32NjYSsvlUExp0+wLrAfsR1stc1cyuBS4rVXnsOT26oFG7uD2O/YCp7p4zs3WA64AaQo7yXxJSXO4NbGNmE4BqMxsTj20mcKC7N6aeDBEREZHuojMu/BluZrVm9ixwM3AvcARwgrvvALxrZvnG7WR33xN4E9ggLpB+H7Cvu19E6H0cFcsOjvXmb4sssN6OVWPcvwm9k/fG7ZsCV7j7HsBo4Fh3f4mQMeh0d3+fMLx+lrvvDKwEbJ18VkRERKRby+UqOvVWbjp7uNyAZ4HdgFPM7NL4OH8m8nMsZxPyhgPUEXoViy0yXG5mGxeVaesMFw6X9wOeiQ3Oj4FzzOwnQI4wj7RU7OR4/xPIsJiaiIiISDfS2cPl0+LP0YRh7YVm9v+AHeP29q6zaq9ZvhBYC8DM1gdWXczjmkto2PYCLgBucPdHzewIYEQs08KXPb3d7HowERER6Wi5lq7dn5n1AK4FtgLqgSPd/e2C50/iy3Tej7j7/5pZBfAh8Fbc/qy7/zzL/jujkTnczGqBZmBF4OS4nxfMbDowFRhHGEJvzwQzu4NwAVApLwKzzWwcYcj9vTbqWjUeV47QU/o88C9gTeBqM/uE/8/efcdJVZ1/HP8sywJLV7DGHvXBgprYQEWQYIsxlpjoT41iL7FGgyYxaqLGElvQaCwxxijWxGgSJRZEVFTsDXiMBSEgKgjSl22/P84ZGcdZlnOZXXbZ79vXvpi5c5577tzdHc8+99zzhLmYvWP7F4HLzGxp+xQRERFpqfYHOrl7fzPrB1xFuO8FM9sIOAzYkTA2esbMHgQWAK+6+77L23lJB5nuPhpYvYGXby14PjQv7ty8x9fmPd4tr32/Iv3VEE9WwfahRbY1VEPu7vhV2P4m4Kb4dM287YcUthURERFpTF3zz5vchXCPCe7+gpltl/faFGAvd68FMLMKwhXibYFvmNlTwELgTHf3LJ2r4o+IiIjIyqk78EXe89rczdfuXu3uM8yszMyuBF5z93cJ96pcGhN9vwXuzNq5Kv6USJZJm9Pbp/9FU1XbMTlmSrFbmRqx/aKa9CDgyU5dkmM6lqf30z3DvJZ/nZ7+h1hdWfr5Bjisx1bJMQ9Nz3AiMuib8Q/pDD9GzM/Q1ynbnZMcc/3LlyfHXLbtr5JjADpm+GUfUJP+czQtw6dz14xZkskV6d/dD9un/xKuUpee16jP8JPXuzY5BIAZGX4Fs5zzLhk+v7Iur1iVIS7L73rXDO/pvYauLy7Fp4uW9daLr9osU1TprYA7wOcQpi7mtItXgQEws06ElYDmArnVfF4GagDc/Vkz+4aZlS1lXfEGKZMpIiIisnJ6DvguQJyT+VbuhXiDz0PAG+5+Qu6yOXABcEZsszUwOcsAE5TJFBEREWkWK6Diz4PA7maWK6t9lJn9FHgPKCcsMdnRzPaO7X8OXCwOmPMAACAASURBVAbcaWb7EDKaQ7N2rkGmiIiIyErI3euAEws2T8x7XGxdcoB9StF/yQaZscTjfcB4wmi5Ajja3ScuLW4p+zvF3a8vLB0ZX7sMmOjutzcQezuhTOXjwCNAF0IloTOBDwij9yrgx+7+8TIcw1CgT/5d8CIiIiIp6tvYqtulnpM5yt0HuftA4ELgyuXYV0NrY6ZYC+gdy0HOAkbE4xtAGBD/shmOQURERKTNacrL5asAk8zsZOBIQgWdZ939ZzHTWA2sD3QkZB33BdYjrHt5CGHx9BsIg8GizKycsJblukAv4FF3z79l9GZgEzO7iVDO8mvHF/dzEPATllQYOgg4Ie8YxgH9zOwxYDXgRne/OfWEiIiISNu1AuZkrlClzmQONrPRZvY84Zb4BwiVfU539/7AB7n1mYBJ7r4HoVLPhu7+XcIl7X3d/RJCvfCTC/Y7OlbtOTRuXxd4wd33JCw4elLB8ZxMqHl+Qnx+aNzHy8Aw4NG4fVNgn1jb3IE9ixxDNbAncADxrisRERERKa7UmcxRubmTZmaE7OFA4Cwzuzw+zw3jX43/zmbJJNRZFJ+EOqrInEyAz4HtzWw3wlpQjS1GNyI3r9LMvkO4dX9j4FPgL2Y2D+jD17OeEEos1cfyk50b6UdERETkK1ZAxZ8VqinXyfwk/nsK4cadgcC3gJ3i9samvy7Ld2IoMNvdDyPU4+wc131aFpOBDmbWA/g14RL9sYQSSrl95O+rjU3XFRERkVKqry9r0q+WptSZzMHxcnYtYYX5n8Y+XjKzz4CpwIuES+iNGW9md/L1muf5ngTuMbMBwHzgv8DaS2l/aFyMtCYe34mEDOhzhMzqfEI2NbeP3DE8sQzHKyIiIiJRWX1bu5++iVy37uHNciJXyVAuLUtZyW9lLCv5eqf0v1uylOnLUlaye216Rxm6AeCVjumR69U2T1nJRc1YVjLLT9G77aqSY5qzrGSWMoK9MvzeZikr2T7jp9AqGX7Qm6+sZLrmLCuZ5feie4bjy3q/SJbPsAUZrnFmKSs5vTz9u9s944k4dcqdLSLN9+YG+zbpWGGrSf9sEe8zR2UlRURERKTkVPGnRPosrk6O6dVhUXLMp7WVyTEHnp4ec+wN85NjAG46ID2ufn565mrGC8khPPv56skx71Zky2X+ZNXPkmM6dk3P+3Xolf5HcXn3bL/2d4xaKznm5EvXT4659LxJyTFZspLnvnJRcgzAmC1+nhyzzXbTk2Nef3nN5Jj+Z3dJjgGYfEv68R28X2P3WX5dfXX6z3jtJ/OSY/47pmdyDECPLguTY25cmN7XVrXpv4PzMqaEslz9Sj/jkOHiDZ3apSfdjvllr/SOWhDd+CMiIiIispyUyRQRERFpBi3xDvCmpEymiIiIiJRcq8lkmtkGwJssWcQdwiLtvynS9nZCqco1gT7ufq6ZLQbGEta+7Apc7O4PLqW/XQlrcL5pZtPdPX2ClIiIiEjU1hb0aTWDzGh8LP2Yxee52LgA+7tm9g93b+hbfjRhoPpmxv5ERERE2qzWNsj8CjMbRKgmlCtluawZx+7A1Fgmch3gRkI5y17Ab4ApwF7At81sPNDRzEYA6wEzgYPcPf12chEREWmzdHd5y7a5mY3OfQHfSIhdNcaNIWQnH4jb+wBXufvuhBKYP3H3V4CRwDB3n0y4vP4Ld98F6EEojykiIiIiDWhtmcyvXC6Pmcx8S/sTIf9yeXdgbBxwfgycZ2bHEIpLFCvg8Lm7T4qPpwOdsxy8iIiItF26u7x1WQSsBWBm6wOrLmPcXGA20AG4CLjD3X8MPMWSgWodS85PG5uqKyIiIrJ8Wlsms9DLwGwzexGYAHy4lLarxkvs9YT5l+MIg8o1gOFmNp0wF7N3bP8icJmZLW2fIiIiIsukrc3JbDWDzHi5ul/BthpgvyJthxbZ1qGBXd8dvwrb3wTcFJ+umbf9kGU9ZhEREZG2qtUMMkVERERas7Y29661z8kUERERkRZImcwS6Vaevmzmm3XdkmMWNHTRfyk2vXNqckwfVkvvCJj6yKzkmC/mdU2OqSivTY6ZVZ4cQvf6bH+HjZiZXiCqamb637ifTk7/ubvqvHWSYwCqnvo0OWbx4y8kx3SuXys5pmOG9MCYLX6eHgTs+s6lyTG+w2nJMU9Xpn889x35fnIMwMJFPZNj3r2nLjmmIsP/cWYv7JUcM6e+2CIhjSufl+E9lafPsZuX4WNl7epsObCZ7dOPryJDVzMzfG+zDEBm35GtPkrnEzOFlVxbm5OpTKaIiIiIlJwymSIiIiLNoK2tk6lBpoiIiEgzSJ+Q0bq1ikFmYY3yuO0yYKK7316k/e3APcDjwCNAF+BvwJnAB0A5UAX82N0/Xkq/p7j79WY2FOjj7ueW6C2JiIiIrNRW9jmZawG9Y83xWcAIdx/k7gOA+4BfNhJ/XlMfoIiIiLQN9ZQ16VdL0yoymUtRbma3AusCvYBH3f1Xea/fDGxiZjcBzxfErgJMAjCzg4CfsKSk5EHACYQqQTcQqgP1M7PHgNWAG9395qZ5SyIiIiKtX2vKZA42s9G5L+BQoBZ4wd33BHYBTiqIORkY7+4nxOeHxviXgWHAo3H7psA+7j4IcGBPd78E+NzdT45tqoE9gQOAM5rkHYqIiMhKq66+ab9amtaUyRxVZE5md2ALM9sNmAN0bGQfI3LzKs3sO8BDwMbAp8BfzGwe0IevZz0BXnX3+ljjvPNyvxsRERGRlVhrGmQ2ZLa7n2BmGwPHm9myTkqYDHQwsx7Ar4H14vbHWXLZPH9fLfBvBBEREWkt6lrgvMmm1NoHmbXAd81sADAf+C+w9lLaH2pm/YAaoBtwIiED+hzwatzHrLx9jDezO4EnmubwRURERFZOrWKQ6e6jgdEF23LLCf2hSMjQvMf9Yvvbgdsb6OJHDfS7W5Fti4ANGjxYERERkSJa4h3gTak13fgjIiIiIq1Eq8hktgbPtk+/F+gHq3ySHOPTeyXHvPNZeszqFdn+2hqxeJXkmMoMfW1ZVZscM6lTTXLMenXZfkV2XrwoOebDdp3S+6lNP3d1H05JjgHYrCr9XLTf9BvJMe8/vTA5ZkBNY/f8fd02201PjgHwHU5LjrFxw5Nj9v/Wmckx3U7bJzkGYNrxryXHvNQpPUex1cL0qe1V7dJ/xqvLsn1+VVd3SY7ZvC79PMwoTw5hfobzANCrJv2cf9Y+va/u6R/JTMvw8frp1G7pQSx9Hl1zamsVf5TJFBEREZGSUyZTREREpBloTqaIiIiIyHJa5kymmQ0i1PseT1g/sgI42t0nLkPsdHdfM+tBpjCzh4Eyd983S/9m9i3gEqAnsIiwpNFp7j61KY5XRERE2gbNyVy6Ue4+yN0HAhcCV5b+kLIzs3WBrsAqZrZRhvi1gLuAM919J3cfDPwVuKK0RyoiIiKyclueOZmrAJPMrC8wnJDdnAkcDcwDbga2AN4nlns0s9uBXvFrH+A8Qs1xCCUff29mGwB/ImRK6wlZxDfM7D1gLLAJMAroAewAuLv/OO7jGEKpyIWEuuVnx+0dzeweYF3gzfjaS8BB7j7JzH4Yj2MacKu7e+5Nuvs/zOyhePyjgc/ie9/T3TPcTyciIiJtkTKZSzfYzEab2fPAbcADwC3AT9x9EPAIMAzYG+jk7v2An/PVWt+j3H0nYGdgQ8Ji6bsQqvH0JWRHh7v7rsDphAEnhAXQzwN2BU4DbgB2BHYxs55m1g44lJB5vAc42MwqY2wlcI6770wY4O4b93tEfH1ofB8bAu8BmFllfK+jc9uiEe4+RANMERERkYalZjJHufshAGZmwPNAF+CG8JQK4F1CBnMcgLtPNrP8hflyWcLNgGfcvR6oNrMXgM3j9jEx9vV4CRxgprtPjn3Pd/fx8fEXQCegP6FU5IjYPjfo/BMw2d0/itvHAgbcBDxrZrcC3d397XicG8a+FwKDYh/5C+o5IiIiIol0d/myy60k/iZwRMxkDgP+DUwkDPows7WB/BWZc9niCcRL5WZWAexEqD0+ARgQt28D5AZ4ja0oeyxwrLvv5e57EUpF/iS+tk6cb0ns8213nwO8AlwD/Dm+dgdwnJltmtupmW1LmOdZePwiIiIi0oDUTObgePm4lpA1/CnwFnCHmeVqGBzj7u+a2S5m9iLwETCjcEfu/i8zGxQvvXcA7nP3V83sbOCW+G8FYZ5lYzoQLp0fnLf/58ysk5ntRJgrOtzM1gHGuvujsdktwEjCPFLcfYqZHQZcZWbdCBnSWcDuy3yGRERERIqoa1uJzGUfZLr7aGD1Bl4eVKT9z4psG1rw/OwibSZRZFCXvwRRweNt4sN1isRsHh+uW/hafH0s0L1g2xuEOZvF2g8qtl1EREREvkoVf0RERESaQV0bm5NZVl/f2FRHWRaTttk9+UT+c+Yayf0szvDz+VrZguSYdcs6pXcETKMqOaZThqnBG9Z3TI6ZW5Y+nbZrfbZpy6tnWHvgo/bpv4t90083i8uyfch9Ud54m0LrL04/EW92Su8oyzvaflF1hih4ujL9b/P9a+clx/R97ZrkmI92PSk5BmD4gp6Z4lKtVp9+7rIs47Eww+86QMcsn0XV6T99MzP8Li0sy/b/6q716ce3Zk16X/PapfeT5dN1XPsMH3rATZPubxGju3+seWiTDrr2nz6iRbzPHJWVFBEREZGS0+VyERERkWbQ1panUSZTREREREquZJlMMxsEnJi3WPtBhPrm4+K/84C93H1EA/G3A/e4+8jlPI61CRV6jnT3++O2oUAfdz93GfdxCnAYkJu09bi7X7Q8xyUiIiJtW13GOfGtVZNkMs3sEEI5ye+4+9GxUs9WwPebor8CRwG/Z8lC7EnM7CTCwvC7xdKW3wH6mtkepTtEERERkZVbyedkmtmPgVOBIe4+Ky7efiLwS2BrMzseeAq4lbCI+gLgkBh+gpkNA3oAJ7n7ODM7lVAesp6Q6Rwes55VhHrmawFD40LuZcCPCRWDHjKzLd397bjv/mb2JGFdzAuBKcC17j44Hve/gF8RBqeD3H0RgLtXm9nB7l5vZhsA/yQs7v6Iu19R4tMnIiIiK6m2tp5PqTOZA4DjgVX5+gD2EkLt85uBK4FL3b0/oYb4t2KbV+Kg7zpgqJltTqjis0v82j/WTAf4yN33jG2Pj9u+A7zl7p8Bt/HVbOZ8YAiwD3A98DZQaWbrx5KTvd39NWBVd58BYGYHxEHyC2Z2ZdzPmsAeGmCKiIiINKzUg8yPCdV6rgXuNLOG9m/A8wDufp+7Pxa3vxL/nQ50BrYE1geeBEYBvYCNY5vX4r9TCOUfAY4DNjSzkYTs58Fm1iO+9qy717v7p8AXcV9/Ao4gZD9z9cvnmtmq8dgejFV+LgB6x9c/dPfFy3xGRERERAh3lzflV0tT6kHme+6+yN2vBxYTLpHn1OX1NwHYHsDMDouXxOHrmWQH3iHMjxwE3E6olf61tmbWG+gH7Ojue8WM6N+AI2OTXH9rAl0J9dTvAb4HHAjcHdv9AbjWzDrG9uWEDG2uv5b4fRQRERFpUZpyCaOjgRNYUozjfcINNGcAPwN+Hi9FHwbcVWwHsY74k8CzZvYysAkwtYH+jgD+5u75BSJuAU6Ox1BpZqOAh4ETYlZzHvAGMN7d58Q+hwNjgcfN7CngJaAyHrOIiIhIJnVlTfvV0qisZImorGSgspKBykoGKisZqKxkoLKSgcpKBm2xrOTdax/WpIOu/5t2V4t4nzmq+CMiIiLSDOoy/UncemmQWSKjP0vPSv5o0ynJMR96r+SYY3f/Ijnm96Mrk2MADqhKzzB+o3xhckyvVdPf08jZqyfHzMk4oWRAtxnJMYPK0//A7bVj+j1oHffYNjkG4NlfpP+87vrMqY03KvDS7jcmx2TJ1vQ/u0tyDEDfke8nx3Q7bZ/kmCxZyfXHpJ87gJ/vf0xyzIT/rpYcs/V2/0uOqZmf/r19b2LvxhsV0b0yPUv2TLsejTcqUJEcAWtlyJhmlSUrWZEhPzc9wwjk6uOy/b9JVgwNMkVERESaQVuboKja5SIiIiJScspkioiIiDSDlngHeFNa5kGmmV0FbEuoeNMZ+AD4zN1/WKTtBsCW7v4vM7sT6AvMItwE2gu4wt3vWJ4DN7OdCeUpd4yVejCzi4FJ7n7rMsRXAOcBewGL4uY73P1PjcRdCbzu7ncuz/GLiIiIrMyWeZDp7mcBmNlQoI+7n7uU5kMIdcX/FZ+f5e5PxPjewJvAcg0ygWOBqwilI4/NEH8ZUA30d/c6M+sGPGpmY9z9v8t5bCIiIiJf0daquSz35XIzuxboH5/+FbiZsHB5JzN7vkjIWsCCGHtnfLwB4Ya7+4F9gXXivwuBe/OO9Xh3H29m3QlVeLYE3jGzVdx9Vmx3kJkdSlhA/VRgPWBvdz8u9vkGofTlgcDG7l4H4O5zzWyAu9eb2RDgYsIg9EagBvg58BmhhOXr2c+YiIiIyMpvuW78MbP9gbUJ5RwHAEMJtcV/B/zV3f8dm15lZs+Y2WTgCuBHebt53933IFQEWsfd9yZU5fle3O8MwiXtM4HcWhGHAve7+yLCwPTovP29F0tKngDcAPwT2NXMKs2sP6GkZQfCpf7a+D5OidWHXjazU+J+Ktx9AKHc5OXAYGBPllxaFxEREVlm9U381dIs793lmwHPxBKNi4EX47ZCZ8UB2ymEQWn+QnOvxn9nA+Pj41mEjOG/CCUeHwYuYEmm+VhgFzMbCewMnGRmufcyBsDd3yQMWquBB4H9gaMIpSZnAKvnYtz9+lgb/c9ArvSFx3/XBma4+yx3r4/HIyIiIpKkrZWVXN5B5gRgFwAz60C4bP5fwmDwa/t294eBR4A/5m1e2uB7N2BKzHReDlxsZt8Cqt19gLvvFQevUwjZToAd4vF8C/gwbrsVOJJw49KomAF9GPhNbqBpZp0ImdPc8eQGtJ8Cvcwstwr6dks9IyIiIiKy3IPMh4BpZjYWeB4YETOIbwI/MLOv3XkOXAhsY2Z7LsP+3yBkKccClxIGmscR5n7mu4WQJQXY2MxGAdcBJwK4+3uES+R/i9lIgLMIl77HmNnThAzlBOArBYNjJvRY4HEzewIt+yQiIiIZ1DXxV0uTPGBy99vzHtcT5koWtnkZsPj0/oLXqlhySf0/edvPznt8ZV7I4ILdP1GkvxHAiEaOe3DB82rCzT0XF2n+RH4/7j4K+PbS9i8iIiIiSygrJyIiItIMWmK2sSlpkFkiU9un39c1++POyTGrrTo/OaZuQW1yTOf6bDOIe9YvTo75tKZTcky3qqrkmMGVnyfHAIybv2p6zBe9k2OGbPy/5BjapX+f3rngvfR+gDc7dk2O6Tf8t8kxOy/qlhwzuaIiOebu3y9m587pPxMLF/VsvFGBace/lhzzn8r0fn6+/zHJMQC9/7HUGhRFTd76/OSYTWeUJ8csmpv+vV1j1bnMmZv+uTJ7YcfkmAUdkkPomuE24E3L0j/7AT6oS///TFVZ+udKZYbRU4b/bXLjTXWc+H8L0gNlhdAgU2QpsgwwpXXIMsCU1iHLAFNah9Y+wMyYv2m1lvfGHxERERGRr1EmU0RERKQZNPeczLhM4w3A1kAVcGxccSf3+nGE4jU1wMXu/q9Y/nsEoXLiNOAod8+UQm4Rg0wz24Cw7NGreZtHAbj7b5Zjv7cD97j7yOU5PhEREZFWaH+gk7v3N7N+wFXAfgBmtiZwGmH9707As2b2OHA+YUnK283sXMIg9Jqie29EixhkRuNj1R0RERGRlc4KuLt8F2AkgLu/YGb5BWV2AJ6LS0tWmdl7wFYxJnfX5qPxcasfZH6FmQ0CTnT3Q8zsI2AiYbH0q4CbCaPuRcDxQDlhPc6PgXWAR939l3n76k6o+tMT6A3c4u43mtmOwO+BMmAqcBih9vrwuG0moS56B+BewhzWinhcbzXl+xcRERFZTt2BL/Ke15pZe3evKfLaXKBHwfbctkxa0o0/m5vZ6NwX8I2819YFDnX3M4ArgeHuvlt8fFlsswEwFNgeGGxm+Yunb0y4bL4H8D3gp3H7zYS5BjsSFl/fjFA96Ccxq/oIMIww2v8C2JuQWu5eurctIiIibUF9E38VMQfIXxeuXRxgFnutGzC7YHtuWyYtKZP5lcvlMZOZM8PdZ8bHfYFfmNk5hGxjbmHGN9z98xj7IksqDgFMB84wswMJJy+38Noa7j4BwN1viLGbATeYGbHdu4R08SaEMpq5SkEiIiIiLdlzwL7AfXFOZv5V2HHAJWbWCehISLS9HWO+C9xOSK49k7XzlpTJXJr8aQwTgXPigPQE4IG4fTMz62xm5cCOwPi8mLOB5939cMJl9dxKVdPMbBMAMzvHzA4AHDgi7n8Y8G9gEPBxzIRezJK5CiIiIiLLpK6sab+KeBBYZGZjCfMqzzSzn5rZ9919OmF64DOEm61/6e6LCOOcQ8zsOaA/cH3W99uSMpnL6mzgxjjyrgROj9sXEwaQawAPuPsbMRsJ8M8YcxhhnmWNmXUkDFJvM7M6wnzOa4HJwB1xsApwTIy518zOAGqBzHe8i4iIiDQHd68DTizYPDHv9VsI0wTzYz4B9ipF/y1ikOnuk4B+BdtGA6Pj4zXztn8A7JnfNi6B9Im771Owj6F5T/sU6folYEDBtlcImctCQxo6fhEREZHGtLXa5a3lcrmIiIiItCItIpO5vIplQkVERERakraWyVwpBpktwWZVDSwesBQvV/dKjpla0XibQqdslx5073Pvp3cEnPr0Rckxda88kRwz+aKXk2M+ntU1OWZCZbaPhB/UpFfgKstwXWHauM7JMe/XdknvCKgub7xNoSmPFp+JvjS1pMd82D79+3Twfh2TYwDevSe9r5c6ZblolN7PhP+ulqEfmLz1+ckxh72RPjW9+t6rk2OoqkoOWXT9x+n9AB0qapNjHqqalRxzRNla6f1UVCbHAPRs4G6QpckQkumyaMf0/21S1rNb442kxdAgU0RERKQZZBhXt2oaZIqIiIg0gyxZ4tZMN/6IiIiISMk1SybTzDYCriDUFV8ALASGufs7zdD3twmLkW7j7rPittOAnd394IK2o4HO8Rg7A4+5+3kFddQPAF5092lNfewiIiKy8mhrN/40eSbTzDoDDwNXuXs/dx8M/Br4Q1P3DeDurwK3Ela1x8y+CZxEWIi9mFy1nx2BQWa2XcHrp6Pa5SIiIiJL1RyZzH2BUe7+fG6Du48zs93MbEvgasJgtydwmruPNbOPCCvSTyAMEIu1OQY4BficUO3nXuAu4I+EOuPtgPPiou6/Bcaa2V7AT4GT3H12zFBeHuNvLjjujoTa5dOATQHMbB9gG0JFoF3cfTEiIiIiy6Ct3fjTHHMyNwTeyz0xs4fiZemJwLbAWe4+hDCQPCo2Wxc41N3PALYobGNmvYFzgJ2BPYDcmizHAjPcfVdgP2K21N1rgSMIxd5fjQPPnE7uPsDd/xqf3xGP713gU2BGrqG7/xt4nZDt1ABTREREpAHNkcmcAnx5ydnd9wMwsxeA94FfmdlCoBswJzab4e4z4+OpRdpsDIx39wVxX2Nj277AADPbMT5vb2a93H2mu7uZTSQMNPN5wfMj3H2imbUDbgOGAc9mf/siIiIiUNfGcpnNkcl8CBhiZl9W5DGzjQk3Af0VuMDdjwTegi9XYc6fGzu8SJv3gD5mVhkHgzvEthOBu+Ocyr2B+4HGVsotOg83FpWfCnQo0l535YuIiIgsRZNnMt19npntC1xmZmvFPmuA44E+wENm9gnwP6B3kV3cWdjG3WeY2eXAM4Q5mZVANXATcIuZPU24OeeGOFhMcYeZ5cq1LAAOB7bKe31sbLOHu3+euG8RERFpo9ra3eXNsoRRrC1+SJGXHiHMsyxsv2be46sL25hZe2Btd98uPh8DTHH3KsLcy4aOY1DB89HA6IZez/NlO3c/DzivoT5EREREpJVW/HH3GjPrYmavEu4Mf5GQ1RQRERFpkdrWjMxWOsgEcPdfAL9Y0ceR4x3Tp2kettrHyTGT/rdqcgyrrJYcYhXFZi40ruZvf0qPeXdqckzvb9Ykx9ROTP8e9ahZJTkGoEP72uSYzptXpsf0Se9n7sMLk2MAXi3rmByz3n7lyTFT70r/GF6lLv17W1+d/jMEUJHhU3Orhenv6Z2O6R1tvd3/kmMANp2R/n2qvvdrF6EaVXHwT5NjqK1Oj7n+rPQYoKY2/eeoT0X6Z3L7DG+pz+JstwLMzxD2efqPA50zXAeenuF3qd3mW6QHyQrTageZIiIiIq1JW5uTqbukRURERKTklMkUERERaQZ1ZY23WZk0yyDTzDYCriCsjbkAWAgMc/d3mqn/dsC5hLUzawlzb09z97eao38RERGRtqbJB5lm1hl4GDguV7/czHYglHwc1NT9R8MIa3AOdPc6M9uesPamuXuGKdgiIiIiadpaxZ/myGTuC4zKDTAB3H2cme1mZlsS1sBsB/QkZBfHmtlHhOo9E4BbG2hzDHAKYTH2xcC9wF3AH4FNYvvz4lqYxwPb5hZmd/eXzGx7d682s4HABfHQOhPW2VwM/BOYSVjLcx5wJGHO7rPu/rMmOE8iIiIiK43muPFnQ0IZSADM7CEzG00YRG4LnOXuQwgDyaNis3WBQ939DGCLwjZm1hs4B9gZ2APoEuOOJdQ93xXYj5AtBejs7l8pL5lXG30L4HB3H0zIuP4wbl8T2MPdr4jHdbq79wc+iIvBi4iIiCyz+ib+ammaY7A0Bdgu98Td9wMwsxeA94FfmdlCoBswJzabkTcInFqkzcbAeHdfEPc1NrbtCwwwsx3j8/Zm1guYZWbd3T23f8zsAODJuP/hZjYP+AbwXGzyobsvjo+PAs6OpSyfZ0mNdREREREpojkymQ8BQ8ysX26DmW1MuAnor8AF7n4k8BZLBm/5S0kNL9LmPaCPEfPHBgAAIABJREFUmVXGm3p2iG0nAnfH8pB7A/cDs4C/ABeYWVnsfydCVnQR4XL8Ue4+FJjWwDEcB5zo7gOBbwE7Lc8JERERkbanrom/Wpomz2S6+zwz2xe4zMzWin3WEOZJ9iHcgPMJ8D/CzTmF7ixs4+4zYlbxGcKczEqgGrgJuMXMnga6AzfEG31+B1wEPG9m1bHt9919sZn9FXjRzGYBnwBrFzmGt4CXzOwzQubzxRKcGhEREWlDdONPE3D3ScAhRV56hJBRLGy/Zt7jqwvbxDmRa7v7dvH5GGCKu1cRbtwp3F8tDZSgdPefAsVqnfXLa3MrIeMpIiIiIsugVd7A4u41ZtbFzF4l3An+IiGrKSIiItIita08ZisdZAK4+y9oIDu5Iswqq02O6dA5PaY8y4/onLnJIZVl5en9APWzvkiOqfm8JlNfqSq7Lm68UYGKWY23KaaqJv1Xq6xT89xPNqe2IlNcxwxTuOsXp39vu7RLj6kn/T3VfjIvOQZg9sJeyTFV7dK/t+mfDlAzP9vP0KK5GX4mqqrSY2ozLEtcnu3nNYsO7dPPeufabJ+VzSXLjRcVGf43U5vhR699lhFX1aIMQbKitNpBpoiIiEhr0hJvzmlKzXF3uYiIiIi0McpkioiIiDQD3V3eBMxsI+AKwtqYC4CFwDB3f6c5+o/H0AmYBFzl7r9rrn5FRERE2qImv1xuZp0J5Rqvcvd+sXzjr1lS8rG5/AC4BxgaF3AXERERaTYqK1l6+wKj3P353AZ3H2dmu5nZloQ1MNsBPYHT3H2smX1EqN4zgbA+ZbE2xwCnEBZjXwzcC9wF/BHYJLY/z91Hx26PBc4AVge+C/zLzAYBl8f4m4HJwCWEGzvfB04gLPR+a+y7N3CLu99Y4nMkIiIislJpjozehoQykACY2UNmNpowiNwWOMvdhxAGkkfFZusCh7r7GcAWhW3MrDdwDrAzsAfQJcYdS6h7viuwHzFbamabAF3c/Q3gNuAnecfXyd0HECoL3QIcGMtHTgWGEuqk3+PuewDfo/jC7SIiIiJLpbKSpTcF2C73xN33AzCzFwjZwl+Z2UKgGzAnNpvh7jPj46lF2mwMjHf3BXFfY2PbvsAAM9sxPm9vZr0Ig88uZjaSUJt8p1g/HcDjv6sBawH3mRmEDOZjwL+BM8zswNh38y3aJiIiItJKNUcm8yFgiJl9WaYxDvDWAf4KXODuRxLqg+eWc80fkA8v0uY9oI+ZVcb5lTvEthOBu919ELA3cD8wl1DScoC77+XuewKXAScX9DWDUBt9vxh/CfAUcDbwvLsfHvfXPCtmi4iIyEqlvon/a2maPJPp7vPMbF/gMjNbK/ZZAxwP9AEeMrNPCAO83kV2cWdhG3efYWaXE0pJfk7IOlYDNwG3mNnTQHfgBsIl7lfc/fO8ff4ZeAN4Iu8468zsdODfceA6h1AHvR640cwOA2YCNWbWMdZJFxEREZEimmUJI3efRMgmFnqEMM+ysP2aeY+vLmxjZu2Btd19u/h8DDAlDvyOKNLP3wv2P41weTx3DLntjxEukef7lDAYFhEREcmsJc6bbEqtcjF2d68xsy5m9irhzvAXCVlNEREREWkByurrW941/NbomvUOTz6R61ann/u1WZQcs0rXhckxTyxaNTkGYLeK2ckx1TXlyTHzFqfff9W1Q3VyzLvVXZNjAKZXpE/d3aPj5403KgGf2zNT3Hsd0qdw79t5ZuONCsyaU5kcM7Gsc3LMFsxPjgH4tKZTcszM9uk/4+9U1CbHfH9R+s84QGVFelyHDMfXXGzc8Exx9251fnLMuAyfK+vUp39+zSnLlgPrW5X+WZTl86tThsPLclPI9zeZkiEK1njq6RZxP8XJG/yoSQddN0y6r0W8zxwtSi4iIiIiJdcqL5eLiIiItDZt7dqxMpkiIiIiUnIlyWSa2Sjg3FgusgPwGXCRu18ZX3+aUA7yjQz73gs4xN2HmtkkQunHOqAT8AqhGtAyT1Q0s6FAH3c/t2D7ucCQuO964Bfu/oqZXQgcCkzLaz7M3celvhcRERFpu+raWC6zVJfLHwMGAOPiv/8B9gGuNLNOwLpZBpgN2CM3qDSzXxIWTT9reXZoZpsD3wd2dvd6M9sG+AuwdWxytbv/cXn6EBEREWlLSjXIfBz4FXAV8F3gVuByM+sBfBt42sx2By4GFhEWNT/a3Web2VXALnE/I9z992a2GaHG+Pz4NauBfq8GJgBnmdlAwoCzllCu8oT4/v4MrE8oB3lqLtDMVgP+AZxPWJh9PeBoMxvp7q+b2Q6IiIiIlEhbWyezVHMyXyOUeSwDdgWeJlTTGQIMAkYCNwMHuvvA+Pp5ZvY9YEOgH2GgeaiZ9QUuAs539yHAWBrg7guBTrHfW/L2PxUYCpwITHL3/vF5rqb5GsDDwE/d/Ul3n0HMZALPm9lEQqWgnJ+a2ej4dV320yQiIiJtlcpKZhBLMr4B7AVMd/cqM3uUMFDbmlDecY67T40hY4DfAp8Az7h7PVBtZi8AmwNbEC69AzwHbFasXzPrTqhNvhqwFnCfmUEoM/lY3P5oPMa3gbfjnMy9gI+Jg+xYS32Oux8dn28HPGJmT8WudLlcREREJEEp7y5/HPgFcVAHPEu4VA6hNGP3WLscYCDwLuFS9y4AZlYB7AT8F5gI9I9tt19Kn8OAe4EZhLrm+7n7IMJl86fi/reP+9/IzEbEuL8AhwO3mlkXYCtCffLcKsvvAl8QLr2LiIiILLe6Jv5qaUo9yNyFWAvc3RcDs4ExMVN5HPB3M3uOcBn9Inf/F/ChmT0PvAA84O6vAicDvzCzJ1lyiTvnMTN7KtYr7w78xt3rgNOBf5vZ2Bj/NnATsFG8u/0O8mqgu/t44E7gGnf/OzAaeDEe33+An7n7FyU8PyIiIiJtRskWY3f3j4Cygm375z1+gjBPszDu7CLbPibM7SzcvsFS+n+McIm80KEFz1/Oi7k07/ElhAxo4X4vbKhPERERkWXVEudNNiUtxi4iIiIiJaeykiIiIiLNoCXOm2xKGmSWSJaUcNe69PuKPirv1HijAuv2nJ0cs/DT5JAQV1WRHFPZsTo5Zvbizskx06s7Jsd81r6s8UZFbF6V/p6q25UnxyxcnH6+16uYnxwD8Eldt+SYLj2qkmNentMrOWZG+qmjR5eF6UFA+bz0/01UV3dJjulYkf6p0r0y/XwDzF6Y/rvRoSL986umNv09dWif3s+9W52fHANw8Ju/SY55a7tfJsdUZhhpbFiT7bNoTnl6XE2GflatTb8MPKFDej/1tdnOg6wYGmSKiIiINIO6es3JFBERERFZLspkioiIiDSDtpXHLNEg08w2BK4EehFqhL8BnOPuc0uw70nAZMLC6O0Idc+PzLrvWPGnj7ufW7B9Y+D3hHPSnrDU0c9jNaPFfLW85Xh3PzlL/yIiIiJtwXIPMs2sklAH/Fh3fzFuOxK4m6/W/14ee7j7orjvy4GjgOEl2nfOb4Hr3H1krIX+d2A/4EHg81hJSERERCSTujaWyyxFJnMf4OncABPA3f9iZieZ2R2E7PC6QFfgCHefaGanEhZJrwfucffhZnY7UAVsQKhDPjRW//mSmbUDegIey1DeBnwTKCfUF7/XzEYDnwGrEAaJfwLWJ2RYT4276mdmudrmN7r7zcBHwFAzm0uom/4jst1kJyIiItLmleLGn42A94ts/5BQted9dx8MXAhcYWabAwcTSlDuAuxvZhZjPnL3PYHrgOPz9vWYmT1FqBg0i1Ai8gRghrvvRChTebGZ9Y7tR7j7kLiPSe7eHxjKkhKV1cCewAHAGXHbeYTSlpcSaq3/GegRX1vVzEbnfW2beI5ERESkjatv4v9amlJkMqcCOxTZvgkwBhgVn48FrgG2JGQWn4zbVwE2jo9fi/9OAXbO29eXl8tzzGwzYplKd59rZuMJWU0AzzUDHo1t3gbejnMyX3X3ejObDuQWXNzN3a8FrjWzroQ5pr8CzkKXy0VERESSlCKT+RCwu5l9OdA0s2MJl6zrgFzWb2fgHcIA8B3CoG4QcDvwVmyTMgyfAAyI/XUD+hKyp7BkUf0JwPaxzUZmNmIp/VxhZrsDuPs84F3C5XsRERGR5VbXxF8tzXJnMt19npntC1xjZr3iPt8E/g+4FtjbzPYjzJsc6u4fmtmTwLNm1pEw/3Fqhq5vBm4xs2eBSuDX7v7pkivvANwE3GZmT8f+zyBkUos5GBhuZpcCi4EPgJMyHJeIiIhIm1eSJYzc/X3g+4Xb44DvWncfWdD+d8DvCpoPzXt9JDAyPt6ggT4XA0cW2T4o7/Eiwg1G+V4ueH2D+HgCsHsDfa1ZbLuIiIjIsmprd5er4o+IiIiIlFxZfRuro9lUrlnv8OQTWZnh1C8sS4+Z3C59JaZ+VeXpHQHn1UxMjtm+83rJMWuWdUyOaUf6yduiOtt5mJfhz7cp5bXJMZ3r0zuy6uQQAOoynL+5GU7fzHbpvxhd69OPbVKG3wuAigznYfMMP0dZPpkXZkwbLMjwufJQ7cfJMX0qVk2O6UyWc5ft/2uVGfIuF798SXLMVduenxwztyzbjLvNF6e/pyyfX19k+F3vmOHbNL5dtlslbpp0f4af8tI7aP3vN+mg64GPHm4R7zNHZSVFREREmkFLvDmnKelyuYiIiIiUnDKZIiIiIs2grU1RTB5kmtkg4D5gfN7mz9z9h8sYvwGhlGS/1L4b2e9ewCHuPtTMJgGTgVpCtnYmcKS7z82476FAH3c/tzRHKyIiIrJyy5rJHOXuh5T0SErvyypBZnY5cBQwfMUekoiIiLRVbW0Jo5JdLjez0cDrhMXOuwM/dPePzOw8YP/Y143Af/JidgcuBhYRso1HAxXAvYQMZAVworu/ZWanEta8rCdkQofH0pK3AfPj16wix9UO6Am4mVXE9t8kLM5+tbvfG4/9M0KJy/2APxFKX1YAp8Zd9TOzx4DVgBvd/eblPWciIiIiK6usN/4MNrPReV8/i9vHufsQ4HHg/8zsW8DewI7ATsDmENb/MLMyQtWeA919IPA0cB6hDvoXMe40oLuZbU6oyLNL/NrfwkrvFwHnxz7HFhzjY2b2FKG++SzgDuAEYIa77wQMAS42s96x/Yi4n+OBSe7en7BA/I7x9WpgT+AAQuUgERERkWWmspLL5muXy81sH+C1+HQKsCZghIFnLbAAOD3OyQToDcxx91xJyTHAb4FhwCaEmujVhEznloTM4pOx7SrAxsAWhLKUAM8Bm+Ud0peXy/OOcTPCoBN3n2tm4wlZTQg11YnH/Ghs8zbwdpyT+aq715vZdKBz46dIREREpO0q9d3lhZMNJgInxUvW5cAjwCnxtRmELOVa7v4xMBB4FxgEfOzue5hZf8LA8wzgHWDvONA7E3gr7r8/oQTl9stwfBOAAcCDZtYN6At8GF+ry2uzPfCQmW1EGOQ+VuS9iYiIiCyzrIUCSsnMKoE7gdWBuYQboz8raPM7wpXj9sDN7n6Lma1KGKe9HZs96O6/X1pfWQeZg+M8xnyVhY3c/XUzG0nIMrYjzMmsiq/Vm9lxwN/NrI5wSXsoYTB3r5mdQbg7/Dfu/oaZPQk8a2YdCdnLqcDJse3PCHMqv5K5LOJm4BYzezYe76/d/dNYYz3nJuA2M3uaMDA+g5BJFREREWntTgLecvcLzewQwlTF03MvmtluwMbu3j+Oud4xsweAbwN3u/upRfdaRPIg091HE0a/S2vzx7zHlwKXFjTpF197gnj5usCQIvv8HfC7gs0fA7sWabtBA8e1GDiyyPZBeY8XEW4wyvdywetF9y8iIiLSkBZyd/kuwBXx8aPArwpef55wIzeExF85YfritsC3YxLuU+C0eCW6QVqMXURERGQlZGbHAGcWbP6EcIM1hMvlPfJfjMm0RXFFnr8QLpfPM7OJwCvu/oSZHQZcBxy0tP41yCyRRRlK0q9Tnf4Xzefl6R1tWZf+bZ5TnhwCwLnlmzXeqEBFTXo/CzOc7yw/7J9l/A3pUZses3l1+kmvyPBH8dSM76ljhr46ZYjpUZf+ze2S4bbKrWqznYh5GdbkmJHx9ylVRca4rhm+T0eUrZUc0746vZ8ssv7eVmb4Obpq2/OTY8565TfJMddk6AdgRoZzUZ7h56FXhs+8DB/9DKjpmCGq5Wjuij/u/ifCsoxfMrO/A93i027A7MI4M1sFeAAYHa9IA4wi3MQN8CDQ6A+yapeLiIiItB3PAd+Nj/cGnsl/Md4Y9CRwm7tflPfSrcAP4uPvAK801pEymSIiIiLNoIWsZXkj8Jd4E/Ri4n0oZnYFIXu5M7ARcFy8QRtC1cRzCTdGn0wogHNsYx1pkCkiIiLSRrj7AuCHRbYPiw/HAdc0EL5bSl8rbJBpZuXALYTFz2sJo+Q5wB+BroTKQB8R7l5amLDfQcB9wHjCXVGVwF3uft1yHOtoQnnLiVn3ISIiIm1bS1gnszmtyDmZ+wK4+87A+cDVwM+Ax919T3ffg5COPTHDvke5+yB3342wyPtZZtazRMctIiIiIo1YYZlMd/+Hmf0rPl2fcEv9R8BBZvYeYWLq2UC9mXUiZCd7EDKTw9x9tJn9N7azGP8Dvq4bIVNaE2upXxefLwKOIwy0/wnMJFQkehr4PSGTOhU4LO7nAjNbA+gC/J+7f1CqcyEiIiIrvxayTmazWaF3l7t7jZn9hTDwe4AwGXUEIaM5jXCL/NqE+uJrErKfh7KkdvhGwK/cvT+wGktKSw42s9FmNgq4CzjV3ecRLs+f4u4DgRsI2VPivvdw9ysIVYGOcvcdCQvF59bk+be7DyYsXLrUdaFERERE2roVfuOPux9pZucALxLKRN7h7rfFUkbDgGvd/Qdm9gfgbsJScMNj+Ax3nxIfTwE6xcej3P2QIt2t7e65VezHAJfFxx/GakAAa7j7hHhsNwDEspO5W/WnEwalIiIiIsusudfJXNFWWCbTzH5sZj+PTxcQ7uw/nXADEO5eBbwDVJlZX6Cbu+9DKAuZu4kn9bs1zcy2io8HEgq9w1dXFZhmZpvEYzzHzA7I2JeIiIjIl+qob9KvlmZFZjL/DvzZzMYQspNnAC8BN8Q1mBYCnxEKuX9OmBN5BGFNp2ylD8IczOvNrIxQbOCYIm1OIKwDVUeojX4teYXjRURERKRxK/LGn/nAj4q8tH8DIV+bB+nua+Y9zr88PrqBPl8Ddi3yUr+8Ni8BAwpeH5T3+h8bOD4RERGRBmkJIxERERGR5bTCb/xZWVRk+ONkYbuy5JjKDP1UZJhoXEv6sQF8lOFElGfoa/3q9H7aZTh3q9Rk+6vzow7pf7+tsTi94FiW71Lv2mx/W1Zn6Gzt6trkmGkV5ckxdRmObV7GP7HXzvCzNz/D7/qU9un9rJXlmwRsWjY/OeahisrkmD6LmyevMacsW/G+DWvSz9/rHdO/T9dsmz7j68xXfpMcA3DfVul9Lcrwbcpyxmsz/Lj2rq3J0FPLUacbf0RERERElo8ymSIiIiLNoG3lMZXJFBEREZEm0GSZTDM7FxhCmKpRD/zC3V9ZelRJ+r0d+DZh2aN6wns80d3fybi/DYB73L1fY21FREREGtIS17JsSk0yyDSzzYHvAzu7e72ZbQP8Bdi6KforYpi7j4zHsjdwEXBgM/UtIiIi0uY1VSbzU2A94GgzG+nur5vZDma2I/B7wk2xU4HDCLXAPwNWAfYh1BTfhHAp/zx3H21mA4FLgFrgfcKC6YcB3yXUMf8mcLm7317kWFYF5gGY2VnAIYSF2Me4+zlmdiGwE9CVsDj7DwhrdbYn1FL/D7Camf0DWAt4092PK9F5EhERkTairWUym2ROprvPIGYygefNbCLwPeBm4Ch33xF4Atgshoxw9yHA0YR65LsC+wF/iNV5bgEOdPeBhMHp0BjXw92/F/s6N+8QrjCz0Wb2JLAXcE4sTfkjwoByJ2ATM/tebD/B3Xci1D7fG9gxttmcMCDuTih32R/4jpmtXqJTJSIiIrJSaqrL5RsDc9z96Ph8O+ARoKe7TwBw9xviawAeQ/sCA2LGM3d8qxMyiPfFtpXAY4SM5uux3RTCADHny8vlece0C/CCu1fH588AW8SXc/0bMM7dawn11E+PczI/cPdZMe5TQvZUREREZJnVa53MktgKuNHMcgO/d4EvgHfMbBMAMzvHzA6Ir+fWcZ0I3O3ugwgZxfsJl9L/B+wXt18CPBXbp3y3JgI7mln7mB3dNR5XYf/fNrN2ZlZhZo8DHRP7EREREWnzmupy+d8J9cNfNLPnCPMafwYcD9xmZk8D3yJkN/PdBPSJr48FPnL3OuB04N9mNhY4GXg7wzG9BdwHPAeMAyYB/yho8zowMrZ5FrgLqErtS0RERKRQHfVN+tXSlLW11G1TuXK9w5NP5OrpFfcyUVnJIEtZySznDrKVldywmcpKzipf+cpKZnlHK2NZyY1UVhKAiR2ylZXcuqp5ykr2qE8/DytjWcksP64bLc5WVnKvT+7J9stRYjusPbBJB13jpj3dIt5njir+iIiIiDSD+haYbWxKGmSWSOcMPze9a9L/IvukfYZvWVn6HzZzMiYcutc1zx9R09qn97NGhj+Aq8vKyPKWMiREMmUYO2XItHapy/YhV5PhPZVl+EDNkBjKdL4712Xra2aGn71eNekdda1vvoTEB3Xp9zL2zPCLMT/D50qWj6L1a9rRvTb9nM8pT39Pmy9Oj5mR4WM8S0YS4EdvpmdA79gmva8s/8+YW5b+Pfq0UzlbLE7vS1YMDTJFlqKZxsyyAmQZYErrkGWAKa1Dax9gtrUpiqpdLiIiIiIlp0ymiIiISDNoiXeAN6UWO8g0s0GEJYfGE9aprATucvfrEvZxITDd3f8Ynx8M3AZs4u7TSn3MIiIiIg3R5fKWZZS7D3L33YCBwFlm1nM59ncscB1hvU4RERERaSItNpNZRDegFuhrZpfGx4uA49x9spmdBRwC1ABj3P2c/GAz2xBYFbgUeNXMLnH3ajO7HegVv/YBhhGqAbUDrnb3+81sIHBB3FVn4Ah3fxcRERGRZdTWLpe39EzmYDMbbWajCNV3TgWuAU5x94HADcDVZtYX+BGwU/zaxMy+V7CvY4Db3P0L4HngwLzXRrn7TkA/YEN33xnYDfhlzJxuARzu7oOBh4EfNtH7FREREVkptPRM5ih3PyR/g5ndGss/AowBLgP6AC+4e3Vs8wxhYJiLKQcOBz40s30JGc1TgHtjE4//9gW2NbPR8XkFsD4wFRhuZvOAbxDKToqIiIgss7a2GHtLz2QWM83MtoqPBwLvAhOBHc2svZmVES5351/O/i7wkrvv5u57ufsOwBp5+8lVxJoIPOXug4DBhBuPPgBuBY5y96HANLJV8xMRERFpM1rjIPM44PqYrTwdONPd3yIMCJ8DxgGTgH8UxPy1YD+3ErKZ+f4JzIv7fgWod/e5MfZFM3uOMDd07ZK+IxEREVnp1dXXN+lXS1PW1m6nbyo3rHt48oncYHHzlJUsT47IXlayuX6aMlRyy1RWMmvFn2kZJqL8P3vnHSdJVf3tZ5a05LCgBAkS/BIUJIpK/gGKgAklKCo5iaIIEgSVl4wJQViy5KCACIqYAMkgGRQOOQgoSTIL7O68f5xbOzVNV9WtO9PDLN6Hz36o7qlTt6r7dtW5J6acX0pbyWkTv6SUtpKzT5rUWubZhDme0lYytePPawm/jZS2kv+arv1FvSdhDgFMmzCPHk84v1knN+/TScqtKLXjzysJbSXHJlxTSlvJuRO/25FqK/nCCLWVTO3488WnzhoVHsgPvnfVnj4m7/7PDaPiOgtGe0xmJpPJZDKZzLuCHJOZyWQymUwmk8kMkWzJHCbeSjBQPzR9+49/lgTXzL8TvuWF30xbbT08ffsPYsaEoSYlfN4vpMQNJJLikn4+6fzafxAzJy6k30qQeXaakXF9T9dehFcSZACmS/j8npm2/UXNm+Bif2VMmqfsjb72cimhJClzPOXzfi3xc0jxSM+SIDNNwjVNSDQJpbi+v3p7exf7sSu0H2fuhEn0WMqPfRQxGuMme0m2ZGYymUwmk8lkhp1sycxkMplMJpMZAXJMZiaTyWQymUwmM0SmOkumpLWAK4DNzey80vt3ArcCs5nZ5yvEO481K/AAsJiZvVJ6/3bgi2Z2fxeZrYAlzWzvoVxHJpPJZDKZ/y1yTObUwb3AFsWL0Lt8ZoBYBTPs+zJegP0LpWOtCDzfTcHMZDKZTCaTycQx1VkyA3cAH5A0h5m9gPclPwtYSNK/zWxeSbsAX8NbRl5jZntKWgLv9DM98BqwOXAicChwajj2NsAJAJJ2BT6PJ6++GLYzmUwmk8lkWpNjMqceLgQ+F3qVrwJc1/H3rYHdzOyjwEOSpgV+DBwa3jseWN7MbgTmkrSgpBmAdYELJY0BxgHrmtnquKK58ohcWSaTyWQymcxUztRqyQQ4GxgPPARc3eXvWwN7SDocuB4vKKiwjZn9qrTvybg19GHgYjN7E0DSm8A5kl4B3kdaOb5MJpPJZDKZHJM5tWBmD+FxmN8Ezuyyy/bATma2JrA88DHgHoI1UtKXJX0j7Hsm8FngS7j7HEnLAp81s82Ab+Cf1ajqCZrJZDKZTCYzWplqlczAecCCZnZfl7/dBfxd0uXA08CNwJ7APpKuBL6Mx3FiZv8FDBhbOtYDwKuSbgb+DDwFzN/Da8lkMplMJvMupr/H/402+vr/x0y3veLnC23Z+oNMaS2W0lby6XdhW8mU1oMzJXx2qUxIOL+RMpOPZFvJFEaqrWTqdEhpc5iymp9z0ki2lWwv81rCRU1qL5L0eafGNSW1lUyYSCltiFPuk6mMVFvJlGdgylwF+M5jZ44KT+Sicy/f02/yoWdvGxXXWTA1x2RmMplMJpPJTDX094+gtWMUkJXMYSJl2syUsJ5JsR68P8Eq+e/FG/HEAAAgAElEQVRp0xZDcyR8EH0plqGE00tZPk5MXBOOSzDZpIyVYuVJXUa/Ok17mXkTTENPJdyVUqxJMyTe659LOL/ZEuZDilUyZT4AzJjwWaRYZ1O8CZMSfhcpFkmAuRKsxynem5T7Q6pq8lLCF5Vildzl1vbWz11X2qu1zBpvztBaZjQxeRS6tHvJ1B6TmclkMplMJpMZhWRLZiaTyWQymcwI8L+WB5MtmZlMJpPJZDKZYWeqtGRKWgu4AtjczM4rvX8ncKuZbVUhtzfe0WcyHpq2r5ndUrHvIsC5ZrZqx/uHAfea2alDvpBMJpPJZDL/M+SYzKmHe4EtiheSPoQXZ++KpKWBTwPrmdn6wF7AKb0+yUwmk8lkMpn/RaZKS2bgDuADkuYwsxfwtpBnAQtJ+jLwLeAN4H5gB7wg+0LANpIuM7PbJa0CIGl54Gi8jNsEvFvQFCRtAuwHPANMjyu4mUwmk8lkMtHkmMypiwuBz0nqA1YBrgPGAQcA65jZasALwI5m9ixuyfw4cL2ke4GNwnFOBHYNLSiPBX7aMc4RuJv9E8Brvb2kTCaTyWQymamfqdmSCXA2MB54CLg6vDcG+IeZvRxeXwWsL2lx4CUz2wZA0krApZKuAOY3s9tL+x9WDCDpvUHuufD6uh5fUyaTyWQymXchk7Mlc+rBzB7C4zC/CZwZ3u4HlpZUxGeuCdwHLAuMlzQ2vH8f8CLuIn9S0rId+xc8B8wuaZ7weuVeXEsmk8lkMpnMu4mpWskMnAcsaGaFYvgs8APgCkk3AHMD483sQuBK4EZJ1wJ/BPY0sxfxGMxfSLoa2A34dnFwM5sIbA38UdJf8JjMTCaTyWQymVb09/i/0Ubf/1oQaq/42UJbtv4gU1rhvZXQYm2eiSPXVnK6BJmUtpJvJrZ7bEtqW8k53oVtJZ8fxW0l5xzlbSXnTJgPb4zQfACYNkHupYT5kNtKOqO9rWRKHN1obyv55SfPHKGnRj3zzrFUT5Wuf79wz6i4zoKpPSYzk8lkMplMZqrgf82wl5XMYSJllZlilUyxbjw6XXuhuRNW2gD/TbBuzJHw4U1IWJ3PkPDbTrG8APw74Zc1doTuPYlfLZMT5t7jCabt97/Z/oN4ICGIZeyYtAV/yk3zyQSheRK+qJR5B2mWzJTfU8r5pZzb7Im/23sS5tHsCeeXYmlNsegCvJzgKpo74ceeYpX8xc2Ht5b5yYrfby2TeefISmYmk8lkMpnMCJA7/mQymUwmk8lkMkMkWzIzmUwmk8lkRoAckzkVIul84GYzOyy8ngW4BdjUzO4o7bc33rlnMp5ku6+Z3VJxzEWAc81s1Y73DwPuNbNTe3ApmUwmk8lkMu8K3i3u8p2AnSUtHV7/GDihQ8FcGm8ruZ6ZrQ/sBZwy4meayWQymUzmf5LJ/f09/TfaeFdYMs3sWUm7AidJ2gdYDFc6rwSeAeYEvgwsBGwj6TIzu13SKgCSlgeOxhNvJ+DF2acgaRNgv3Cs6YF7R+TCMplMJpPJZKZS3i2WTMzsElz5OxXYyswKlf5sM1vXzP6DWzI/Dlwv6V5go7DPicCuZrYmcCzw047DH4G72T8BvNbTC8lkMplMJvOupL+/v6f/RhvvCktmidOBmczsidJ7BiBpceAlM9smvF4JuFTSFcD8ZnZ72P8q4LBCWNJ7g9xz4fV1vb+MTCaTyWQy7zZyCaN3H0VZ3mWB8ZLGhtf3AS/iLvInJS0b3l8z/K3gOWB2SfOE1yv3+HwzmUwmk8lkpnrebZbMSszsQklLATdKegVXsPc0sxclbQ/8QlIf3oxh25LcRElbA3+U9Dzw1jtx/plMJpPJZKZuRqNLu5e8q5RMM7sSuLL0eq2Ovx8MHNxF7jZgjS6HXDX8/W/ACsN3pplMJpPJZDLvbt5VSmYmk8lkMpnMaGU0lhnqJVnJHCb+O2Zy804dbL3cE807dfD8/WObd+pgwQv2bi3zs0+e3FoG4JvfnaO90BtvtBaZeM+jrWUmvfBma5mzbnhfaxmAjca82Fpm8UMSjOUTXm8t8sLJf28/DnDa4wu0ltntlG4Ognoe2emi1jJPT5irtcy23xvXWgbghdPvbC3z9BOztpYZP+0MrWV+uv2MrWUA+l96pbVM3xztr2nM0su0luGNCa1FXhr/1/bjAP2T+lrL/OCxeZp36mD1ie2/27knTWwtAzDPmGlayzw2Xftx1niz/TX9ZMXvt5b5zi3/r7VM5p0jK5mZTCaTyWQyI0B/zi7PZDKZTCaTyWSGRrZkZjKZTCaTyYwAoyEmU9KMwJnAe4CXga+Z2TMd+1wMjMMr6rxuZhuEeuOnAv3A3cDXzaw2VnBUKpmS9sY77EzGL2ZfM7uly36LAOea2aoVx1kL+BXwz3CcGYGzzOzojv0+CSxkZicM42VkMplMJpPJjDZ2Bu4ysx9K2hxvm71bxz6LA8uUuieCd0Pcz8yulHQc8BngN3UDjTp3uaSl8faP65nZ+sBewClDOOTlZraWma2NF1r/jqRB2SlmdllWMDOZTCaTyfSSUdJWcjXgsrD9B9yoN4XQ6XAO4BJJ10gqWnCvCPytSq4bo9GS+TSwELCNpMvM7HZJq0haE/hB2Gcm4KvAlHTh8PeD8Q4+DwI7djn2rOHvEyVdCTwDzAmcAyxhZntL2g/4LP7ZjDez4yV9A/gSbg0918yOGu6LzmQymUwmkxlOJG0LfLvj7f/gHQ/B3eWzd/x9euAnwM+BuYBrJd0E9JUsm93k3saos2Sa2bO4JfPjwPWS7gU2ApYBtjSzdYCLgS8WMqFTz4nA581sTeAJYKvw53UkXSnpcuAs4BtmVtTrONvM1sUVTyQtD2wAfAT4GLC0pGWAzXDNfzXgs5LUq+vPZDKZTCbz7qS/x/91YmYnm9kHy/9wBbOoQTYr8EKH2L+B48xsopk9DdwGiIE23VVyb2PUWTJDYOlLZrZNeL0ScCmwJ3BUaAm5AHBtSWweYD7gV0H/mxH4E3A/7i7fvGI46xweuMnMJgGvAbtJ2hRYGCgKr82Jxyp0ymYymUwmk8mMdq4FPgXchBvWru74+7rArsCGkmYBPgjcA9wmaa3QXXED4IqmgUadJRNYFhgvqag6fh+udR8JbG1mWwFPAuWquc8C/wI+E1pJHkzExTNYKwe4F1hB0hhJ00n6M65M/gNYOxz7VOCu9peVyWQymUzmf5lREpM5HlhG0jXADsABAJKOkLSKmf0BuF/SDbjBbt/gZf4OcICk63GX+vlNA406S6aZXShpKeDGYLUcg1sx1wjv/RePJ5i/JDNZ0m7A7yWNAV7CYzaXbjn27ZIuw7X8MXhM5h2S/gpcI2kGXPNv36onk8lkMplM5h3GzF6jFHJYev+7pe1vdfn7fXgCdTSjTskEMLODcWtkmYuA3bvsvmqQ+ROucZd5GriyYoy1StunlrYPBQ7t2PdHwI9izj2TyWQymUymGy2sje8KRqO7PJPJZDKZTCYzlTMqLZmZTCaTyWQy7zb+t+yY0Pe/ZrrNZDKZTCaTyfSe7C7PZDKZTCaTyQw7WcnMZDKZTCaTyQw7WcnMZDKZTCaTyQw7WcnMZDKZTCaTyQw7Obs80zMkbWdmJ5Vef9PMjqrY9/tVxzGz/9eL88tk3ikk9ZnZuyrrUtK0Zjax9HoOM2vsbZzJSPpq1d/M7PSRPJfM8JKVzB4haWa8z/lbeNum083s0QaZD+LtnuYAzgLuNrPfNcjMBXwCmA5vtTl/KChftf8Hqv4WqvkPGUlbAJ8G1pa0Tnh7Grz/aVclE+/iBPBZ4GG869LKwEItxp2PwZ/D9e3Pvvb4SwCHAa8DB5jZ/eH98Wa2c4XM+Wb2hbC9QWjX1TTOz81st7C9rJndOWwXMcRzC/v+wsx2DdvLm9ltLcacFv9ey9/TOQ0y0wDLAzMV75nZVRFjbQ98C5gxjNVvZosO91gp4wB/BNZvuoaOcfYwsx9H7vulqr+Z2dkR8ssAs+Gtdw8BDjGzv1bsO2/Y93RJX8E/gzHA6cAqEWONCTIfA240szebZDrkpzOztyr+tpKZ3dzmeEFuKHM8Zd4tAnyBwfOucXEtae4OmcciZBbHu72Uf4M7Vux7KBVVd8xs3wqZFIVxqfD/VYHXgOsYuE9EKZnh/rw43vb5iXfbIm5qJSuZveMs4JfAJsA/gRNwZbCOnwNbAycCJwN/AGqVTLx36H3Ah4AJ+A+0juMr3u8H1ul8U9JT4W8z4Dezx4H3AU+b2SIVx7oM7y8/rjTeZODBqpMys+PDeJ83s13C22eF/vGNSDoFv0HNHM7zwfC6av9Das6l680T/w4PxW98F0naMjx8lqw5tXGl7T3x77SJD5W2j6TL99INSfuZ2UFhez4ze6pBJOXcYHC71p/Enl/gQrzn7QL4wuNJoFbJxOf4HMC/w+t+oFHJBHYCPlWSiyFlrJRxXpD0GcDw30bMIu9Tkn5mZpMijr98+P/KwBv4Q3sl/DNvVDKB44Dd8J7G3wOOALoqmfjvbDdA+G8E/Jr+2DSIpMOBh4CFgRXwxebXGmR2wru/TYsrSROBJSp2P4IwP8uLtwiGMsdT5sM5+H0zWkbSCcD/4Z9ZHz5XPxYhejpwCbAa/vubpWbfe2PPp0RrhdHM9gGQdJmZbVi8L6mzi19XJO0KfA6YCzgNVzZ3TTj3zDCTlczeMSdwMfBNM/uqpE/GCJnZA5L6zewZSS9HyuwUlKztaHggmtna3d6XNH3F/vOFv58J7GNmj0uaH/hZzTDzAE/x9h953c2sYJykxczsQUnCLSQxLAksgyu1++LKQh1PAzvj7Uv7Isco2pci6QHgwvC9xq6YY8fpq9huYh3goLB9Fu0ejG3GST0/gNnNbE1JJwHfAGIWEXOb2eotxwF4tsl7MExjpYwzD27tKui6yOtgbuBJSQ+H/fvNrKtSYWZ7wpSH9pR7T+xDG/fA/AOY3sxuCBborpjZRfii61Nmdmnk8QtWM7O9JF1hZmtLqlJky2yH90/eD/g1gz/HTsrz80OVe9XLtZ3jKfPhNTM7oKXMssDiCRa718zsUElLmNk2kq6u2tHMToPuHogamaEojO8pwiwkjWPwQriOzYHVgcvN7EhJf4+Uy/SYrGT2jumB7wC3SlqaOAXreUk7AjNL2hyIimeSNBa34PVHjkMYZ3cGbhpvAZWudGBRM3scwMyelFTnxj4+nEvnzTnmQfot4BxJC+CK6lca9i942cz6Jc1sZs9WKc0F4Ua0IvCkmf0lcoyJkjYGLjUzC6vn3+GfYRV9kqbD3YfFdl84hyq3YH/FdhNtH4wp5zaU8wOfZwAzm9nrTd9T4FFJCxbzr4mSlXp6SX8Ebi3Os8ZK3XqsoYxTtdhrYOMEmfdIms3MXpI0J/EP7X7c4nmppE2BV6t2lHRO2B9JW5b/ZmaVbvvANJJWAR4Jc2GeiHN71syekjSrmV0pqc6tnOoybT3HU+ZDKXzpPyHE4ZaSTJNl+0lgVuClmPMr0RdCHGYNYV1zRcikeCBSFMaDgZslvYQbGLaJkIGBJObiu3ojUi7TY7KS2Tv2AD6D/2i+DOxSvzsA2+JWuGdx19a2ETLHAN8G/oS7sq+JPL/tgbWIswYA/FPSGcBNwEeButVvygO0kL2GiDiuLtwiaQ/c0nMufiNsYntgbIsxtgEOxONFnzezKyR9i3qr7sK4SxRcgSseHP1AVZzWxyQ9Fvafp7Tdb2Z1yn3bB2PKuQGsJunJIDNXabvfzCotHIHfyJO87pB0AzUPyFKoxlhgU0nPFefXMI51/L+g8jNJHCtlnPmBw83sK5LuxxeHswDrmtlNNXLrmtlfJB2BWzT78RCHJg4Fbpf0DP6Q3y5CBmAzYBUzu1TS2uF1FcdFHrMbpwFH47+tI/CQoSZelPRZoD8slusU0wUk7YDPz2IbADM7oVosaY5XzYc6yuFL24d/ULMgl3R9+Pt7gPslPVTIVFm2OzgAdy2fgce/x8Q8pnggWiuMZnYBcIGk9wDPRYaGgC+IrgIWlnQpcFGkXKbHZCWzR5jZtZLuBibhD9L7I8Q+DFwa/gFI0uNm9q+acS4IO84J/NrMYle1bawB4MlLG+Au6XPN7OKqHRUSSkoPbmi4QZdcgAVv4RbCN8xsqW4yZcxsX0mz4HGpG+DKcCUaSAiY0HTsEu81s606xr0C/96qzuv9LY5fMHOCDMCKkq7DP+ulS9tdHz6J54aZxVgfq2SPKbYl/R54oGbfIlRjkGVRUl0MbNnFNyV5I7w+neqYsNZjpYyDK1FnhO1/BRfxisD/AzbsJiBpPzxp7i/AGsAPcNfgvvhito5pzGzRoNw+baXs7wbewBc7mwC/x61dz3fb0cz+JmkF3Lr1LPBd3Op1ZMQ4M5vZR8J200K3YDtgMWBv/Pq7Jt0Fzgbm67JdS8ocL82HVXEF/ShJZ+ExnVUyaweZscBSZnZbUKB/XzPU5qXtIhZzBiKtd2Z2laTb8UXmomb2SoRYaw9EG4WxpDh3vk+M4mxmv5B0Of58utfM7mqSyYwMWcnsEeFB8yc8EHsM8Hl89VjHQcC8uMtkeeBNYKykE83sRxXjrAEci1vufi3pUTM7OeIU21gDwBWfmfHA9DkkfdUqMgUtZCwXD+5IlsRvmMcAx5vZTZKWJ84CTHCvH45fx/nAIgxkrHcjJSGgtYykGfBEgKPwOKYj8YfBHmbWNcjfzCZJ2tDMfi9pVlyZeCOMX5fYtWzENQzp3EqynzGz30qaDdg/yB1qZpVu1SC3DG75mlJBgYrkNnm1hfmBIyTtyUDW8mHUKPaSvo5b6OeU9Pnwdh+egFcl03qslHGAuToXaGZ2i7xKRBXr4gkeAK+b2R8l/QW4sUamYGd8UfhkxL5lTsETwdbEkxBPDttvIyxQ18afJ0/jyugTwJnARg3jtElmKngN9/QsiCew3F21Y2eco6Q5gElm1hjvnjrH8d/TVmF7f+BUfHFQx5n4IuI2PGxpU6BrqEER7ynPYl/azL4tj3c8g4EFTCVh4bAf/n39Sp4DcFCD2G8k7U+cByJFYdy84v0oOj8LSWeYWeNnkek9WcnsHYuY2ZmStm0R0P4asKyZTQgKwAW4cnoV0FXJxBXTNcK+h+Cu3Bglczs8Ay/GGgDwW9xSUVh5Gt2x8mSkQZhZV5eJmb0RZBYr3IZhVa+mcQIn4BaD/fHP6zRqsstJSwhIkTkaeAVXWI4F/o4nVIynYtEh6WBgGXlc19H4YuP+IFOZeWtmj0pazszukMdX7oA/GN/2PaSeWzi/w4AlgiXyF3i83pNBrrJ8SeAo4isozAlsAbyXgQfu5HCulQRr6TGS9jWzyioCQx0rcZwZStsblLZfrxMqKWE/L15LejFivOnlSRDlLPam7whgnJmdIq+gcJ2kuhjf9c1s1WCNMzNbGEDSFRHjzENkMlOJ4/H5th5wM241/lS3HYOF9WQ8BGdjfI6+IC8HdUnVAEOc4xPN7J8AZvaQpMkN+wMsYGbHBZkjIj+7nRnIJt8Qv+/FKFa74/fGy/Dnx80MJAwOItyPHzSzYxRquzZ5IEhQGEuK8/vw8KOl8fCdb0ceIvWzyPSYrGT2junlAfP/lNcyiwl6nsfMJoArXZLmNrM35XXkqphsZs+H1egERWakM1DiZFZcgWxijJlt2bzbIM4L/+/Dy5M0xeuBPwAOxN3dHwMeiRxrrJldLi/jY5Ka3OApCQEpMgub2SfCA3h14Atm9pak79TIrGxm68szOjcGFjSz1yRdWzeQpN2BzSR9HPgx7g57FL9pd7O6ppwbwIpmtl44vw1L5xcVD2yRFRTM7GrgakkrmNmtMcfu4Dh5zdbGGrJDHCt6HNyDsLiZPVD81uV1C+tcltNLmt7M3jTP5C6qQcTcv/eLv4zBFKEC4cFfZ2l8HSDcfx4qvR/ze2mydHZjMTPbTtJqZnaJpL1r9j0Y+FqY1wfhiv0D+OKmUslkaHP8UXkS0PW4cvtEzEVJ+oCZ3SdpMeJiyieVnhdvSYq9P00Oz5f+oDTWWWbPl8cnn4An/0xsckUPUWE8EVfkr8JzBk5mwIpfR+pnkekxWcnsHUfgK7rdgW8Sd7O/KNzEbsLLRVwsaWdq3EHAA/KCuePCzTa2dEZhuezD41geob780Z2SPgLczkD2Y23RZDMr18m7THElLL6Mu5o2AO4h/iH5hqRP4Nmqq9Ica5mSEJAiU1gxPg7cZANFo2esObdCZmXgH2ZWuMjrstjBP7OP4d/Pl4APmNl/5bGZw3Vu4HUJwR+gd5fOLyaOLaWCwvvCHC+UuLnNLMaSXNSQXRZXhJpqyKaO1Wac/YDfSjoRV3YWxb0KX66ROQs4RdI3wvc5Bx7aUFvvMlih/ippFzw8oZ/6JLUy38Tr/C6FX19d2MqM8kLYYzq2Z6qRKZiOjsLgQNfC4CWmDQt35OEkdZbCMWZ2pzwmdeZiARFhXRzKHN8W9yJ8Cr+HNbmiwReBv5LHLz5J82cA/ry4Gn9erECcsQB8MXU2PtePwz0YXTGz5YM1eBvgAEkXAyeaWZ0lsyBFYRxbCie5KCycY/htx2dRmTOQGVmyktkjzOxCfOUH8H15N5ommQMl/Ra/sZ9iZndLmof67M1d8BvANbhLZ/uafctjbVFsB6vIrxpE1mRwCZWmDGQklTuazIe7IpvO61XcBTkb7hq+i8GFkavYAbfezU2c+z8lISBF5tWgjH4RLy4/Bv++6jpzTJJ3StqWMIckrQU0uUcnBzfqCsBDZvbf8H6VqzPl3IrzWx9fDBSJZ+sSpzCmVFD4Pp7RuhNwBR6jGIW1qCE7lLFixwkhIP+Hu1w3xMNPPmX1yX3HBKXoKnns5kvAMRYaGHRD0jb497MG/p3+EneRfhvPOG/ifmAXG0hEqbNevY5buvpL28X7TbQpDF7wPTwsaD7gBrpb6QsKL9An8ZjHIhZ51oYxhjLHLzKzVt2cgDXMrDLOuILz8QQh4R3l7oiUOxyvEHIbniRTZ9ElKOa3hufE54AfSxprpfqrFaQojNNK+pCZ3SXpQ0R6j8zsIEm/o/1nkekxWcnsEfJg+J3xle9MuKVjmQaZxfEHz3TAksFy0bSi/V3CDa2TaWlQGM1sOXlc1jzEl5bYorQ9gYgSFvKaorvige8X0ND9o8TuZhYdC2QJCQEpMriysieuLJ6GJ0hsHN6v4lt4wskjwLHhYfdTXBmsRV53b2vCSl6eaFP1XVWdW9Oc2w2P/30UdxV/Arfcb9p0fsB4M6uz2nXjOTO7XtJOZnaqpK1jBdW+hmzSWG3GMbN/B8va0UXsXhNmNl7S9WZ2e8z+eH3ZIubz5aConowvRmOUzLOIT0QpMqS3NLMzI8+vILoweIkFPSJG8+BVMuoUkb/Iw0wWBD4dXNHjaV5UD2WOvyDp0/g9vxfdnApONrPVcO9SG34f5C5rKTcP8H48OTWmTFOKwvgN3Go/Px5msEPdzpK2M7OTNLj95XKSNrPmmriZESArmb3jk3j7xZ/hCkJtskIgZVWfckMr1wXsw+dBbX26YEk7BbemzSlpezOrrZVmZlsH2QWBac3s4ZrjbwJ8HVfKfwkoQsEus5RC4d+YnZWQEJAiA/zIzLaWtGN4GF4e/lVi3hN9E3nP5DfxKgUflLRaw2Xthwe7PwLsI2lNPGu1q3JqZs8Ce4Xzjzq3IPcgg+sm/pGIFoKBsZKWZfB8bepV/Ya8isJ04WEfW7XgGFxhb1NDNmWslHGuwTPZZ8Xn+3lm1mT5O1Be1PqXwDnWUHrGBrKgzw+vJ0iKKVcDaYko2+PzrQ0phcF3AM4ys2eadjSzw4OL92kze65QMs3sNw1yQ5nj8zA4/jCmCUVKAtSrkn7G4KSuutqfBc9L2q1Drmsok6SZ8J7qX8OT404GPhl5n22lMIbzuB1YWV6Sb2LDAh4GElHvpz5uOPMOkZXM3vFcCK6e1TzRISY+KWVVn3JDa1teCDyuaDXzbj8L4NavrkqmpI/hGaAP410hfgK8JukEMzui4vin43FmPw0Pg01ant/SwLOSnmXgJl2XaJSSEJAi82FJPwK+KGnh8h+qVtryxB0BewZZcLfft/B6iV0xs78DH5G0tpm9Ii81smgp1rKKFCsKktbDY46nZEybWdPc+wCDY8cawy5wj8CS+Bw8EHdpN2Khhmw419gasq3HShnHzM7HkyrmwxeiR+Jxk3UyGweF7CvAnyT908yqiqvPWJI7JpxbH3EJJYT92yaizCDpNgYrL00dfw4APku7wuDlcYrfeuU4ZnaPvKD8Febtap+SdJyZ1XkTALeU4ffX8ufZ5PVZOywGFsPDVp6NuKaUBKgi1roxDKmD5/CyXIV7vh9fIHXjIdwrso/VNAvoRhuFsWMBvxEeItZYBcAG4v43HwaPXqYHZCWzd/wrxEW9Gkz5MT24i1X9LLGreit115EHwzfGZAYFble8luQTeImO9+M34RsqxCZZqLVnZk+oPnv7Z3jppblwl9tieCzT33CXUzcWx928V0u6C4+tjMZC2ZQCSR9tEElJCEiR+RyeWLMR8Z1AXsa/jxnD/8Ef2vtEyh+Af5exrdVSrCjg3/O3GLAmNGKlJBp5maUvRMg8ATwRFi9Hm9mVdftLei8et/cIvgC4GLdM7miDk9GGNNZQxpG3Zf0afv23MLicUR3T4Ur9GAaSU7pxmTzD+Xsld/IBxLtIv4UnorwXv0c0KmTAXpHHBkDSNGZ2FR5rOgtuPW1aEHUbpylRDdwK/C38mXcS8eVtdsYTeGrrxpaR9EV8kXIP7oH4YUQYwSRaZmKb2QGSNsTDsMzMohJ/Cg9TONcP4R6kKhYPC9ZxGug69XXcktzVmpmoMJYX8Afjn/n9NFcBKEjy6GV6T1Yye8eOeBzQr/Hg8bq2bAVFu68ziV/VI2llXGlcnxCkXrPvV8K57IQ/HEXIOLXqsisAL0n6Bp7UsAYV3T8Cr+Yyt+IAACAASURBVAeXL5JuN7Onw3Zl1q2ZPYXHQB0iT4zYPig9F5hZU1eT4tpmwOPGvo63B6y0+pGWENBaxswewfsyX2WRvbfN7E48m/+EWJkO+iX9hsEWpbr4pBQrCsBjFt/3fQrBercTHqN7BxU9kOUJJ8cB/8Jdvl8G/ivpZjOrSyI4A//dzYnP181wRfh0KlyeiWO1HqfEBbiys1qES7A4x7/i8/pk4P+svij4QXhc74OSnsZbEF4MNJWnAsDMbqRUhD4sCKrO6xxgBzP7W8yxg8wH8WSQlc0T1NYFfiJpY2uIUy3GkbQo/lvfkmZr3mfx658eL9V1b+SpPmuhJE8LdsdLIL0SwiEupzmMoHUmdjBeLIGHXnxN0uox90pJ0+BGgF3xz+2kqn1LIRnnMtAC87/UF9pPURg7F/C3hHONqTEKiR69TO/JSuYwo1JZmxJv4HUI72kQn83Mxoft98jrbFaNMz2eWPP1cPzZcNdoU1zX9sB6JSvXncHF3OSy3BKP+TsY72hSl8RTvjGULRN1BZ2nYGZ/Bf4aXE5fadpf0iL457BZGGMzM6sq21OQkhCQmkQA8BVJ38XL28T2+d62NJ9iZaC6+PogNDhYvpOYoPmn5SVQbmOgrFVlTJg8RnRXvEbrZOBjDUr093D3+ux4csPCeAWFppjHsWZ2Yhjzi2Z2ediui0dMGStlHADMbGVJGwM7SLq7yfIZ+JZ5EsW4BgUT8/aRe0g6HFesnm1h2UZeZmp3BkoLTcQVmm5cD9wgT5aKCfEBjwHfPCiYmNlFQRk+ioaMfkmfwufRx2nu/lSe4/fiC8SvyrvPVM7xYAUGr1H6R+BWBuZ4029jcqGcmdnLDV6fgpRM7DXM7OPhfH+OZ9pXErxkO+L31OuBGcystkVriZlDiAdmdnYII6giRWFMrQKAvBLJhjZQZiozishK5vDTNtYRSRvhN8wtgpsO/Ef3GaoVmEdwC9CXzex+SX+IUDAhFOLteO9YPP6s6vyWDCv/PYNiNaMNlMfpRlUP7coe5JJ+SUKxc3nJpzlx69EH8QSKJgUzKSEgRabEpniR7jY3ws/ihadjvtdyyainIo8fa82pokjkmjf8v/L7k3QLvsg6Hrfs/D7CSvuqeXzjS0EReyUcq0lZKruRy1bCurjClLFSxiEc9xi8QcP1wHbBFblng9iCYb6/ENzLOzSFDuBx0//ELWUxyTsF2+MWtf1wa21lX3HzHt2/xysh3IxXKij+VuWyHGNmN3cc5zrV9MSWNwnYCrd+/yQcoylTvjzHDQ/ZicE6/t+GByX9hAGvz4MRMimZ2NNJGmNmkxnoYV7HA7gSv3xQfv8QMUbBm/IY7BtwN/hwK4xVC/jzamSQtCtunZ8oadfIxVpmBMlK5jAT4mQKpYySUlZXUP0O/IHzOgM3tcm4i6KKn+Ou4UUknUSklRC/mc1igzNTb2XgxjAIefzmIZJWMbMXcffKLyXtZaH7SBeKHtpz4q6VGIpr3RkPaL8WL0a+SoNcH24tnTFcQ7Siap4Q0CdpFdwN+ZykNUKc2LDJBB4hrm5gmdtxS1Ks3BYV71cF9k9nZieBJ4VYfSmYKUh6n3ldx65u7gqKDk4b4DF+MWOVH2RtkpIWC5aovo7tOmt9ylgp4xQsZ15GBuDnqi6YX+YHwEfMOyXNC1xEfetUzOzD8uYEW0s6AjjfzA6PGOtZM3tKnrh4pbwkW904D0r6Kd6n+6MMKD1VLssqRbyu4cAe+Jz7ZVDGGl3/ZnYaQPgMVgkK8Vm4kjrscoFtcIvhevjCqq4jUcE38Uzs+fDKIjH1js8DrpUn+H2E+ucFeE3abYHL5TVdYwrLF2yH1yE+Cl+01FX+aK0wlhbwz5nZ0y0W8F/CQ75mw8NXspI5yshK5jCTopQFi85pks4Iq9JGwoPi8OCC3A7P4jscOKNBoT0W+I2kPXFL1KJ4cd6jK/bfA/houJbC2rA6Ht9UdT1FW7GzSg/Spuv5Y5D5jg1koF8rqalM0qfl7cu2BW7Ek6Y+Cfwp8rO8AI9XK/dkb1IYU2SmB+6SJzUVbremzNs78IScJxlwl3+gZv9jOq1DDXyJgXisvxIfw7R7+Hc8A8pirVJhZjtLmhG36J6AJ0TsjFueq+J7Vytd+1yl7Tkbzu9nDCxuytnhP6iRSRkrZZyCxwplXZ5cExN7+7KFsj3mtTZrXeYlbsOT/BbCFZ8YJfNFeZxqf3Cdz1O1o6TZ8fvHEsCaNdbLMn+Q9GPgQDN7MVhmf0h9Ca1FgE1wpXwmvGvU7MW9qYGjcCsowP64MrzGcMrJkzW3xluEjo+9lwd3r5nZyjH7F5jZT4Irf0m8ZmbdfR8zOw84Tx5etC2wqKTz8GfG7xpkHwjPtj58EVE5X7t4fBYlrmzUPfKucOubl5CKsQBPMC+B9mydFTzzzpGVzOGntVJWYi9Je9Eibs88CP5v8sLgX8FXc8vX7H+2vF/04Xjc2SN4Fm1VQPaETiUgrDRj4oyi67GVmEXe7ebvuOWr8cYRrGoHBGvLJ3Cl+wT8odrEvBaXST1UmZgHeydb4Kv0qNqfeOb+OuAxWmZW1wkFBlu/Yy3h4HVfB1U2iCG4/U/DF1RL4t/THbjFo9v+qQ+Nz5vZGpLGm1lT56ehjNV6HA3Upx0LfE7SY3g93coyNxqID5xW3tXkGtzC3xhjKekEPB78N8Cu4eEdw3Z4xYe9ae6gdQfujt8qVrHCYym/i3eSmQlPJDwNt5Z1JYT5nA2cLW9duR1whzw5q6lKwUQLCUVm9pDiE0rayJ2Gu6TnwON7G+OaU9y9kpbCE7teBvZqUi47MU9G3F/SD/CknO2AWiUzGDAewp8ZKwD/oaZRRlAYp5G3NF0GuE/S9NZcE/cFSZ9h8DMjNku8zT0sM0JkJXP4GYpSthkt4/Yk/cLMdjUvJ3F0cOPW7T89A4WFp8Tx1NwA+iXNWI4LDA+Fpj7a0K4eW8E2eHzo0Xg8VUxWPpJ+ap4FfBlevqXS8tLBvZLmt1CeabhlJH219LJou3ermT0UMc5jwAvWkORRonyTjent3V+x3cTpDCiz+0TExU1BXjz6BDO7B09MqSzLVFKu3obVJ1+8LunvwBKSluuQ67o4SByr9ThWUZ82uGUrT6Hj/xDfp/oPwM4WWQNVg1vBglsw/0j9Yu9zZnZb6RhzWn3MNiE04/DwD0lz1Vi0u8nfL+kwPGY0pjrCo+E7vh5X0J+IHKqN3Nxm9gV5e9am+1xBirv3OLxr01z4wjKqK5q6J6UCXBohvpqZ7SXpCvM6oH+NkDkBb97xZ7wt8Ul4O9Vu5/YhM7sLn2/l+N+mLPFl5H3Y+0rbQJSnKDMCZCVz+BmKUvYIkfF38lpl++GuvXLh8qY2dUUB4zKFstktluwo4FJJR+Ir2QXxVoS/aDpHK9VjC+cc07/9XkkHEOrFmVlsfbpBHX8sohtIYHXcdVnsH5PB3UamM9lpFmA/SUeZWVMW+HzAA5IeKI1T5+JrmziVeoMuK7PrEdemsOBa4Eca6HRzLoMrEJRJSboAj/ucH3fn7xIpkzJWyjhTUGTJrSI+sCQ3K+7C3ZlSkk0FjwHXyRsoPAzsZGb/qNm/bVwvhYIZQneOAaaR9GvgUTM7ue7k5N2Vjm0pM2UcPCkppsTQ1njZrA3wOMmDImTA3co74Ba/JrnC8jY5KJoxpLh7J5nZZQDyWsyxVN1/Y+4b0wQDxiPhPGMW8UuU7lcXqT7u+NfyAvmtvCMMbvN5XEvZzAiQlczhp1MpWwh3NzUqZQyO24OaThbmXTyOkbSvmVVaYbrIvb95r0H7F6VFtsMfqI/i3R9qy2UABGVxF9r1b/8m/qC7Ebd0/crMKl1oJZbGk3CeIa7jDwBmVlWWZVhkzOxtljp5n+sraS411HXVX8MCwVrRV9ouzqNbaaHUG3TrKgCl82jT6SY2S76TogTOz3ErUZkqhSRlrJRxUktuIWlpvHTPpnhccIwF6yhgO/NEmeXxBIzKhYoNLtS9PH5d/whWpiYODMe+AK95ey1e77GOgxJkUsZ5C4+VfAa4C890jinpdJHFd5IZI68nOqa03QfEtE6FNHdvrDKLmR1QbKt9EffTce/SNrj1tLYNcWCspJnM7LVgaKmrurAi8OMQY/q1WOOCDdRMnQZfeC2EV1FoFUKQ6R1ZyRxmglL2Hzw7cH5CH+kYpYy0uL1j5Fmjy+BK3IF1bidJ11OhJHRz8YVV683h36D3I26cG9C+f/sWwOpmNjHcpK+jJk6rdO4LN+1TRtJ+ZnaQvJD0oM+jSrFPkak41wmSYh460+F1GydTKq5ds//ZDFgryttVSmFlL/kGxsnLmYzBLelTHsJNMbca6HSzCV7VoK7TTWur2hDkRkRGCSW3gqfi6/hi7ZeAzKwuu7fMhEJBNLPbJMV01EHSgbib8ibgm5J+Y2Y/ahCbbGbPS+oPczymyPxIyRyPZ22vh9/LTsetk0206SSzCG4RL5TFYr+61qkp3oRx4TdXJKlF//4grYi7mR3LwP27spxVB0cCt0v6B24EqEyICyFBOwfL9rWSbiz9Lebemvr9ZnpMVjJ7gJldD1wvaVn8xxybuHEbnsFYtBarrF1Z4mQ8s/lsPO7lVODTNftvHnkuBW3d62VS+rf3mReSxrxjROxD8cO4W2vslBM3q3MlFYlObSx4KTJvQ15+ZuaIXU/As7i/j8+FQ6ipdVhYKiRtZKVsUVUX9T8P/x7nxi07d+Nz7z94cH8Vt+JuXvA5WyhbMTG3Raeb1a2h001nuEUsVXJ14RopY6WMQ1rJrdPxB/ZPzbN1N2kSKLlR35R0FH6PWAWPkYthA7x0z+RgJboeaFIyHwgKzDhJexPnxh4pmcXMbLugUF0S5GKI7iRjZotEHrNMijfhVgZ+c21/f9CiiLuk80OcaZGwVtBvZgtUyJQ9NPfii+X78I50lWWW5MmAh+JenqhudyWK73e1lt9vpsdkJbNHSPoefqP+O/Cd4PY9skHsFLxY8FnEKYwA48zsqLB9u6TaLEsbKC+0OPBFBjp6zE+X2mdt3esdpPRvv0bS+cDVeOzjtZFjnYqHJMS2YdwYuMPM/iZpPvO2lsMu08XqORZPhIpp7zcRuBPvzHFNeNjXjdWtqP80+Bx6W1F/M/tokPsN8FXzAs0z01D/MkUh00BtzS3xz2O+QhmrsQwVssUDrg9PdnjIzCoL+5fkUsI1Wo/VZhxLK7m1OB5TeHUIpZm77nwCxe+28EAsh7uHY92I/8IXHi/i94j/RMjshIfVXIO7puu6woy0zLSS5sZj5melvpj4FEKSyzhgMXwu1FUBqGwoUbXgLbl7+/C6wGO77dchk7T4KtGmiPvLQWmM7XkPsBL+OzgTVyobwwDkVVV2wisg/L7FWAXF90ub7zfTe7KS2Ts2xDPyJkuaFr8hNimZ48ysqFfZqDAGZpQ0r3ndvPcS0W0kcDpumVsNdzPM0m2ntu71DnbE3eVF//ZGK6qZ7RHihZYCTjGzmMxHgH9bKCweyToMBPGfRVyNyBSZTuvE68A9TVa8QB9+o74szIWmCgVVRf2biqa/rzgfM3tV3g6uksQ5UdTWPI4BJQ4iegxbKSNb0sJ4PcUYWodrJI7VahxrWXIrLGYOwevv/h+wvaSHgQuq3Jxmtn/ne5I2wN3uMcyPl525A7duv6mQuFHzHX8JL79WuDq/IOlxM6trzTlSMvvhC9b5cMtdU3kvwNuF4r/5e/Darj80s6o+5KkNJSCh9q68csU+wAzFe2YW0wigTRH3FXCvy5n4NUGD0mhmy8p702+Jl8C6CjjTzB6oEVsJWMnMnos4/250fr+xLv1Mj8lKZu94Gl/NvYJbOGKynVMUxv3x7NEXcUthbKbva2Z2qKQlzGwbSVU9h9u618vMjLuw5wN+DzTGIUp6P241GIPf1D9oA8XZ63gkuEjKfbTrXEcpNSJby5QsFb8ws12L9yWdbmZNiT2b4R1dLsEVsdpyTlYq6h/eGoMXTm6qOPAnSX/DrV6r4KVU6mg9J8zLS72ttmaIwWpznEeDWy2GlHCNlLFSx5kVd33uQklRaDinvwJ/Dda1rzTtLy+Uvi1uJXqcgeL7TXwxcr8ym+P3vKLcz1i8/uOtZvbtd1Im/A4lL232rEV2t8IXRiua2SvBQnY5rnB1GyOpoUQgpfbuXrh3JdZ7Awwq4i7gJKupNmBmyyUojJjX7twbpvzGD5W0oJl1LdVlZinzrSyf+v1mekxWMoeZkpXnPcD9JUtAzAptPwYrjI2txczsz3jnhrnDGDcS9yDpC7GBswQX6VwVx2/lXu/gFLxO35p47OjJYbuO3wIXEt+OsmAG/KZZZPk2xSel1IhsLaPBpaY+j392fUBdGRnk8bxP4cr5nvhCJbabz6G0K5z8PUnL4C7e083sjrqDD3FOdPJjGiw9HSEH8xHnuoWEcI3EsTrHqevRXIxzOu5FeIEBl2VdHGzXuOOafZfDM9HXAs4HnjKz/2uSKzERT0ScJ8jfaWY31oswHbCODZTwudTMPqn60jU9lZEnLh6CJ5rNgBcwP1fSgUXsdwOTLbTgDeEkMfWOWzeUIK1e70NNyl43QrjGDwjZ5ZK+bV6gvSttFcbSOLMBn8NjRgtr6LBS5VWRFONpy4wAWckcfoZi+XuvmS0qae662J9uFPuH2J4YDgA+i//wH6Y50DrKvd7BODM7RdKW5p2PYs7tcTP7YcR+AASX40kJcUorhodSH7B0abu/5ubUWsYSSk3JO3F8ErdEPgG8Gv5/Bs0xutCycLKkBfHwjrHAkpI+Y2a1vaoDKXOik5g5UQ45mEC8sr0jXte1MVxDoXJAGGsB/POuHUsDhfavw/ud341fT0wChyJdm2VOJT7u+CZcgV/GzN6UFBt2UnAC3qd7f9x6dRoNfdLxUI3p8NjP6RhYuNZZaXst8xN8sbaUeSb6bPii7cfEuVQflPQT/DNYg7hWhykNJVajfb3e1yT9AbidAe9NY5chvDvTePya1sIX/7ULkDYKYwgx2AIP/7gQr836SMR5pTCU521mBMhK5jBTsvJ8v8ufmx7cOwBntVUwO4i1yq1iA/Un3xOxf6x7fRCFuzGsnmO6jlwi7+QxxcVrZnUK8PPAb+UJG8cDl9QkUJRZNmKf4ZApOEdeA7Sc/V4VBrCBma0q7/V9r4XyTJIqM8s7aFs4+dfAX2jpdiNxTnRQOV8Lxc/aJWd1dlkqeBGP+6oKHVgHKMa63Mxi4m3LCUFb4BUemhIpCm6SJDNrUwS+TdzxOrib/G55kfOYagZlxprZ5eE7sEgL3jHAnfKSNUsCR0jal/qkkV7LrFheAJrZS3hLxSsjrgdcYdwRL41zD8GiV4d5Q4nv4QlbdxJhDTezD0SeT5m2C4eCsWZ2cdi+SFJVWEKqwngerlzfgXceO0RyB5MNcxeeYfaqZHpAVjJ7R3Fj6cPdYDFFc2eQdBuD+7ZW1Wx8W63GMFasdeRTkn5mke3miHSvh3MrWoTthtf1Wwp3ucV0Rdkcv5kXD/DaB7Z5xv6RklbCM3APkXQhcKKZPVYjV9yc3hYrSUUR9BSZEm3CAF4P470uqdx+MjZjsm3h5JfNbL/IY5dpMye6ubX6cCWhipREK3i78lckPtXNpZR42ymF9iWtGmlFKngR+LukVxiwhjdZrqLjjs3sWjwecFY8UWYmSdcCZ5hZjKX1DUmfwBcsq9KcdIaZnSzpIly5esC83NI0dfeYEZCpKrhe+1sK83lrPKZ+fOTCtZDdFbf6zYVbn5fAQxfqZNbA40zH4L/d/c3s7DoZ/DexFW6tb1OAfNriHi2pqf1sisLYtmvPcDAcXpVMD8hKZo8ws+PLr4Nbo4m9WgxR9aCIrbU2D/CkPEu16JBTF8PSxr1etAg7Ek88acMbZrZzSxnM7GbgZnmrvv1xRX3Gqv2VECuZIlOiTRjAWHkC1JiO7aiEEmtfOPluSZszWHmpLSsUOAB/mMbMicKtNSfx8bYpyVndlL/K/uglUvu4p8qsDcwVGRdY0DbuGPOqAccDx8tjOhvjvAM74C7lufGOZY2/yaCMbk2wJoUYw0+8wzJ9KnXeKdG06D8NeADvRvUBoM0CYnO8/NrlZvZzeX/7Jo4AvoxbaT+OlxxrUjKPo2UB8uD23gc4RV5C7Enq50RrhTEk4Yw0w+FVyfSArGT2CEll98d8VJQnCfu2dgsOww95o5b7t3GvJ7UICzwqaR886zYmSxyYEle4JV7c+B48xrCSlFjJFJkSbcIAJjGgsE3s2K4kuNO7xrI1LCA+HP4VjCVicWBmVzFQZqV2TpSswGeZ2WpNxw4MVfFrI5cSozsU7gfei8d+RmFmW4f7ymJ4a8TGJJEQrlLuGhXbVWx3M2sb73YUXsbpC+H8YhJeei2zCIO78BQ0zYu5zYuQjyGuwHmZQoEtxohpX/k67v2aaF5dJKbaQKsC88HC+h38PvINC/3P63iHFMYUCq/KrE1elczIkpXM3lG2ZE7ArQFVpLoFh8Lbskep75wR7V63obUImw63HBRKeq21RtJWeOb03HgA+7rWrtZam1jJochEhwG0UMI62RsP6v8cDQopgKSN8USSicD3zOzc8H5U7GfJCl7wkpl9uGr/wPOSdmNwSEjV9zuSil/reNtSyEqbloAFH8fd388x4Eloqk/a2g1L965RlzfIACwlaQ4zi+1WBvCCmZ0jaX0z+6G8LNY7KmNpXXhgYG4WGextOBtffC0sT7i6KELmJTwu+tjgMakM9SnRtsD8l3Ar+Gx4EmGbAuujncLTdgn+2f3ynT2dTEFWMnuEhXqAkuYAJll98e0kt+AQaZs92sq9rsQWYQnWmrWB/UIMWgopJZNSZKLDAIKrp6rYeWVdSTO7UV4jc1kz+03EUN8Dlsfn3K8lzWBmp8WcY6CIp+zDrdcxte6ew63My+Ellh6lehGRlGiVovwVltaWHFex3YiZLZEwXoobtlXXqBJLA8/Js52jlGBc2VkGj/8UMG/EOD2VUUIXnsCY4GYfU9ruC3K19X7N7Bfyig4fxBP37qq9GmdT3DL5z3BtMQlebQuQTwjn/qw8IXCqR9IKuHFhFdzQMB6/x9QWss+MHFnJHGY6Jv1G+MPnBUl7mNklFWLD4RZsS9vs0Wj3uobQIqyttcbMvhbk5sPj/Sbisa1Hm9ntEUO2Kpk0BJk2YQBbtTz2FMysqb90mTfN7HkASZ8BLpf0GJFz0MzKbsBr5TUiuyJpaeAXZraOpHvxWpLvo6Yf9hASraqUv2H9bQ3FlRgSLk7BP4N/A9uY2W0NYilu2LZdowCwUNGgJbvjtRePwq1540eBTGoXnoUZ7GYvYpT7aUiuDEribHi1hiMlHWJeRL/bvmPxLOijgJfklQDewD1ftWFGNlCA/D3AM9auAPlIGTN6zcF4SNZbkg7Cu289gNdnvrhWMjMiZCVz+ClP+oPxQOz78UlfpWSOdDwYtM8ebeNeH0qLsBRrDbi19BC8bd75eMxWTNB625JJqTLRYQBm9iBM6X70BQaX5YhtCxjDI5J+imeyvixPZvojnuzQSFAqy4XL69x1hwPfDdtPmdfvXBx373d12ykx0cpquiwxeiwcRwHbmdkd8oScIuGjjhQ3bGfXqE3rdi7iw9WlekVECMC2Fjo74ZbtGHoqY4ldeMzs/XV/b+A4vLLGAbi34AigqlbtUXgG+xh8Dvwdn9/j8cV2JZLWDDLT4J6IR83s5BqRwqqfEt4xWhljZnfKW+HObGa3AkjKvctHCVnJHH46J/0t0Djph1J/MZW22aPR7nUbWouwFGsN+Fy+ihBbKCmmXBK0LJmUKhPCAKbBb/AfZaDvch1n4grYGnhSQGW2fCLb4MlShWX1cUlr49mnMdxb2r6D+hivmcwrAICX78G8BeN0VQKpiVapyukIM8ZCZyUzu11SYwxtoht2LG4tLWohLof3V2+iXJQ+lpQ4zpGSSenC07XLUoObHeAtfK5Nb2Y3SKp7zi5sZp8IFs3VgS8EA8V3Ik7vQPzecAG+wL4W96JVUV5gtArvGMUUz4tP4jGtyJOmGrtuZUaGrGQOP60n/RDcgkNhE2BnM4uNK0wpzpxCirUG/KHxU+CqoCjFzu3oWMmhyEg6nMGtHv9Ns1v8dTM7UNIp1oOyHOblc07teO8/RJQ9CokGffj1PIF/Tx+S9JyZ3dNFZIqCbGafLb3/VsSpnqMWiVapyukI85akjYCrcUWhcTElrwW7FV7KagN567wmheeS8C/2d55SlL4gJY5zpGRSuvBAuy5LBf34fexSSZviHbuqKIwPHwduMrPi9xCzoJxsZs9L6jfvZlQX9z81ZYq34S/y+q8LAp+WtBhuBT7vnT2tTEFWMoef1pP+HbK8TAf8WZLhhcuvbNi/dXHmFDqsNWZmd0aKboXXizsZ+AxuoYshpWRSikyrVo+BPknz4FaYGRklZTkkLYErlb/FQyaWwuv0PY5/9t14QtIqZnZT6Tir0BB3FkjtZ99KOR1htsU9CYfiVvGY+pXjcYWnTUmwJ6xdof3kJMSUOM4RlLlX0gG4gnqfxZdVa9NlqWAzvOTbpZLWol6hfVXSDnjS3FnyTPZtiMsufyCErIyTly9KSV6bqjGzwyVdDDxtXpR/Mbx4fkziY2YEyErmMJMy6d8Jy4t5zcsfS1oZ2FPSiVaf8dq6OHMbJM2OP3j/C5xmZvdI+pCk6yLjUh/Gi4l/BHctfwS3HDbRqmTSEGTatnoEL2u1Gd6x5jG8vNVo4MfAFuUFgKRJwPJWXUXhu8DFQbl+AE+e+D9g44jxUhKtIF057Tlm9miH0hOjILxk7bL/weOHD2Jw/HBdke/kJER1FEkHWhdW76HMN/HuTzcCe0j6lQ3U/a0justSiTeBtYPx4D48fr2KnfBe6hea2amSNsDjsLeKOLddcIX0GtxaGlto/11F2XMS4tljkX0qagAADihJREFU+stnRoisZPaG6YOCOR3uNn9D0hhrbk12jKQj8MzJ+4ADLWT/DjfBMrYJXmOyD6+jV0db93pbfo1bw5YHFpT0H+AH1NcXLXMh7jJfAA+Ef5KBdoKVpMRKJsZXnsZAq8efA0dGyIw1s1+E7d9I2iRCZiSYrYuFeRI1HYnM7OGgZG8MvB//rvc3r6naREqiFaQrpz2njdIjaf2w+aK8R/ctxCs8X8QfukVx78KVW8VQkhBHYzH2gi2A1c1sYrgvX4cvlppo3WUJrxrwN3xRuCbucv90xb6zhmPPLmld3Fo9GU+e/F3DOL8zs/Ub9slk3lGykjnMSNod2EzSx/GbWFEL8Gd4xmEdJ+PxiGfTfHMaKq8ANwFfNbP7I/Zv615vy6xmtq+kPrx0yCPAh83s6Uj52c1sTUknAd8AarNHC1JiJdvIyGt+/gS3tH6Xgezm62uOvyGeVLWlvO4leKzvJniQ/zvN25RJM9tH0g11Qmb2Ot4ury0pyVmQrpyOBG2Uni3C/1/ES3oVHocYhectM2tj4RpKEuKoK8Zeoi/EIBMSa2JigZO6LAHjzOzosH27vHRUFb/EF9OL4FUxPoCHIv2BZiXzBXnpsXJjg5h2sJnMiJGVzOFnAzx7sR/vsPABM/tvsAg0Mc7MjgrbTTenJCTNglv4bsMVn7MlPY27P1+qkktwr7dlQhinX9LrwKfNrE3cZ5GdO7OZva64tmyQFivZRuYUvJTJXPhDYwXgGTwTu0rhuRsvMP0GA3FWk4mPM+01N0raxbxHOgCSdsYXLb0gJTkL0pXTkSBa6TGzrQHk3V2WN7M/y+vJnhkxziOS9mRw/HBlx59It30Vo64Ye4lrJJ2PJ1qtjmdiN6K0LkszSprXvD3ke3HPShXThoScv0lau1hUK6LaAB5yU07S62dkusVlMtFkJXP4mWxmk+RF2R8quZdjgujb3JxSOQz4ddmiI2k7vCj2jlVCCe71tpQVgOdaKpgAF0raH7hD0vWEMjkRpMRKtpGZaGZ/BpC0W2E1lvRKlUB40J8sry6wGK4k3W9md8ddUs/ZBzgtJCw8jMdX3k/vKiEk9bMnXTkdCcpKz2rEKT3nMNCu9nlcyWxqkjATbp0sLJT9xLWVTGF3fBF1FHApHh4yKmTMbI/gIVgSOMXMLo0YB9Lq9u4PXCfpJdwdvkPdqQXvyw5mthVAiAGNSUzaAFjKzG6T9FmgVeOLTGYkyEpmDwjula0JxdfDqrux5zcDN6cX8Y4RlR1UhsByViqTBGBmJ0natkGurXu9LUmxYJJOKb2cBrf4PUlcaRxIi5VsI1OOwy0rzjH9kLfH59GNwH6SzjSzn0XI9ZQQR/kFeS3YhYDHzCzGjZhKSqIVpCunI8GBuHK5FHCqxXXGmtnMzgdP3pHU6AY3s6+UX0taL+Vk69Dgbk4X4IlW0zO4juo7IlOSnQ1YC493f5+kGyLj3VvX7Q2LykUlzW1mzzbsvj2wcUe8/r9wBbqJM/Eyebfhv41Nce9ZJjNqyErm8LMfcAYeU7iPvCvDGTR02oDBNye8/+qNxPWwbUOV8tXVPZPqXk+gsLTMSbts4JVwa82ZeFxbVNmVxFjJ1jJ077LRh2cVN/EV4GPBnTo9bu16x5XMEr/EEyMukXShmT3ci0ESE60gXTkdCX5vZqvRzvr0ZlASb8DbIlYuXCV9BfdavIon/zyEW0GXwxWt4aR1N6cRlClok4xTJrpub/Cg9He8B0DVQjkol7/teC8mDAJgATM7LsgcIemKSLlMZsTISubwszNe37IPX43OiLvEdsAfDo0Uq9+QBDPcPC9pJRvovlIUea5a1Se519tiAwXpzwoP31i5ZSV9EI9X3Bt/IJxpZg80iKbESqbIVHXZiOm40WehOLOZvSnpzQiZEcO8U8lsuNvubEljzWz54R4nJTkrnF+qcjoSPC9pNwYnbTQpwNvhyUFH4clMdW7YPfGF2/y4cjYfnkyy1ZDOujutuzmNoExBm2ScKdhA3d5l/GVtl6XNS9t9uMI5A/Fdy1oj6QNmdl9QtnsRXpXJDImsZA4/K+GK5Vm0sKxV0ItEhT3weoVX4qVN3g+sS3W9wlT3eiqtH74hVnFvAElrAIdKWtDMura9DLSOlUyRsaF12bhe0rkMxO2NJiUJeWbrenhN0sfwvue9ICU5K1k5HSGeAz4c/kGclXUtK3VLkpdBqnKrPm9mz+GdcZYBdjWzS4Z4zlWkdHMaKZkpsinx7sF7cRheZuhueQ/0rslRpYXy9sDSZvZtSX/CPVlndJMZIrsBv5K0JG7YqFt0ZDLvCFnJHGZSLGuSzuHtCmUfnlAx3Of3SEha2TAc/ya833dVvcJW7vVhIOXhW8RcfQ4v9zIzzZm3KbGSQ4mvjEbSeWa2WXhIfQaP2zvXzH7bJDvCHI5/DocBl1m7XtJtSEnOgkTldCQoMsZjkLQF7tpdW95/G3zOfYhqJbM8Vx/toYIJad2cRkRG0oeC9XE/4pNxypyOey+uwxd6pwJrN8jsjFcYAb/PXsUwKpnypNKT8ZCJ/4fX1pwVrxF8y3CNk8kMB1nJ7AEJlrUq12mMSzXl/CYQX2+xrXt9qOc26OErab66/SV9EVcsF8ILsu9kZo9EDJUSKzmU+Mo2TFGigmI52pRLAMxsSUmLAJ/As/tnarAep5KSnAXpymnPkPQUA27UmfBWnAsAz5jZIhVilwFPAeMYyC6fTH1nk7kkrY0ro7OWlNPaEkaJpHRzGimZoyW9D4/H3Bu40uJr7wK8amZ/CNu/l9dBbmJSUR0jxFMPt0fqYOBr4dgH4eEqD+DhEBcP81iZzJDISmaPaGNZG6JLtde0da8PCXmrvV3wrNGZ8M5HdYkK5+HZpXfglp1DSsH2dZmWKbGSQ4mvbMNikrq2FzWzfYd5rGSCReVTuMv8NdIKrdcdPyXRqkyqctozzGw+AElnAvuY2ePyLP26hK6ZzexKSZ0Z/LPUyNyFXzd43dVi8TbsJYwsoZvTCMqsJa+Z+1E8u3z7cH/4m5kdFHF5j0vaD//MVsS7t60fjl3lYfmtpKtxL9EKDL/iN8bM7gzzZmYzuxVAUlNHuUxmxMlK5jAzBMvaqCTBvT5UNgDehz90fwocW7/7/2/vbkLkqKIoAJ8BF4EwIBiFLOIiRo5/C9GFK5UQkJhA3EZQEEWNIroJGNSIP4EhkIUuAgpOJIKgTCAgURFFBI0SQUQQ5QSzMaJRnIWIgqtxcavHVrtrqquqX73qOR8MdJLp6RfSpG6/uu/cNW9djVSnsE/4YeBPRE9q7g4idsT3SKqaSzqJOget2ihOU9gq6TwASPqR5OUl3/sM4tDPy4gicXCoBBgTvj2ILiJ5+9BOHDil0aSqMc0p4XP+IvkF4n00j3gf3VDx6XOIYn0bYvf4Z8T/72PbeCQdInkK0cf5mqSvJllvBYP2nJ2ICCMUhfR8y69j1piLzPbV3VnL1oS315taLi4K88XJ0bHzsIu15bwLXNcFSce7XkQF9yB63e4keRbA86qWPVhVncNZQM3iNLFvGCNDP0fssn1c8r03MTIXtwOrqRNPonx4wm7Egay7medo0iSK29u7AVyMKMhOATgwSG0oed4gum0TIhXkWgCVottIbgFwG4AN8UveIem5pn+XIR+QPA1gC4A9JK9A9GW+2eJrmLXCRWb7au2s2aofSN4L4A+SC4hQ+vWmL837i6iXPVhV3YNWdYvTlB5A7NpfgzjUVXZL9VkA75Lcgcj+fB0Ri1MWF5X7aNJUnkZ8uFhA3CKvOqRhVHTbfagW3baEKGjPT77ctUk6TPItAL9IWh4UmZJOTuP1zJpwkdmyGd1ZS+lBxO3yJcRO2d7S755BkvZ3vYaKamUPTqDuQaskKQANbUTsYG4GcI7ktnEJFJJOkLwIwPuIYQUvSjpa9sOV/2jSVC5FjIXchbir9BPigMw7kr4ved6o6LZFRkbwWn6X9FTtFVcg6duhx+dQfgjMrDMuMi03GxG7PJsR01CyCiC3f6mVPTiBugetUqUANHEMUezcitgRXiwejyTpjaLQvB8x4aaqLEeTplLsXH5YfIHkTgBPADiK8vdrk+i2r0nuRUxJG4wzPVt1zWazxEWm5Waii6916iAie/A3RFvDQps/vMFdgVQpAE1cIukYybskfcqS6V5DObpziF3JT0h+B1Tq8859NOlUFXFrNxdfVyF65Y9j7baBJtFt1yPGdw7+TTcgdq3N1h0XmZabyhdf61bR97iV5CZEiP4ZAK90u6r+tKwwJrWgyHEcO4cczQrlrEeTJnAYMYnqEIAvJVXNrJw4uo3/DFHYTnK/pCPF73umuK1bLjItOxNcfC0Dkn4FVk89WzWPAngVset1AjElZqSGRfNnzHg06bRJ2lHzeXWi2y4berwLMWcemM54YLNecJFpWRga//YY4uJ7NeLi+3CnC7NJ+GK6hv9keB4AcBLAlQCuQ/TwtfU6fRlNmq2G0W3+wGUGF5mWjyWSL0l6Ae5fytpQj+CwOcSOj5Ury/Bsbb41ejKadMasjHlstm65yLRc3AjgCMn3EHN5L3S9IBtrXF9gTgdrcpUqw7MXo0lnTB9SDcyScpFpWSh6nR4ieQuA0yTPDP1ZLyclzaq+HKzJVKoMz76MJp0lfUg1MEvKRaZlozjwswDgI+Qz/s+sTal2u/oymnRm+MOX2f+5yLQskHwcwD4Aj0h6u+v1mE1Jqt2uvowmNbMZNrey4v5k6x7JJQD7JC13vRYzMzNrzkWmmZmZmbWu7WZzMzMzMzMXmWZmZmbWPheZZmZmZtY6F5lmZmZm1joXmWZmZmbWOheZZmZmZta6vwG11dugIpATGAAAAABJRU5ErkJggg==
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#34917;&#20840;&#32570;&#22833;&#20540;">&#34917;&#20840;&#32570;&#22833;&#20540;<a class="anchor-link" href="#&#34917;&#20840;&#32570;&#22833;&#20540;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们对每个存在缺失值的数据列进行分析，然后对数据进行补全</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>PoolQC</strong> :泳池质量。 查看数据可以知道，这里面NA表示没有游泳池。这个很容易理解，因为缺失值的比例很大（+ 99％），而且大多数房屋一般都没有游泳池。</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;PoolQC&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;PoolQC&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>MiscFeature</strong> : 房屋的其他附属。NA表示"no misc feature"</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;MiscFeature&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;MiscFeature&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Alley</strong> : 小巷类型。NA表示 "no alley access"</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;Alley&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;Alley&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Fence</strong> : 围栏质量。NA表示 "no fence"</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;Fence&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;Fence&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>FireplaceQu</strong> :壁炉状态。 NA表示 "no fireplace"</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;FireplaceQu&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;FireplaceQu&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>LotFrontage</strong> : 路到房屋的距离。因为同一个街道的房屋到路的距离应该差不多，虽然没有这个房子到路的距离，但是可以用同社区房屋到路的中间值来填充。</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#Group by neighborhood and fill in missing value by the median LotFrontage of all the neighborhood</span>
<span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;LotFrontage&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="o">.</span><span class="n">groupby</span><span class="p">(</span><span class="s2">&quot;Neighborhood&quot;</span><span class="p">)[</span><span class="s2">&quot;LotFrontage&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span>
    <span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">x</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">x</span><span class="o">.</span><span class="n">median</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>GarageType, GarageFinish, GarageQual and GarageCond</strong> : 车库位置、车库是否修建完成、车库质量、车库状况。我们用None来填充缺失值。</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">col</span> <span class="ow">in</span> <span class="p">(</span><span class="s1">&#39;GarageType&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageFinish&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageQual&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageCond&#39;</span><span class="p">):</span>
    <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s1">&#39;None&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>GarageYrBlt, GarageArea and GarageCars</strong> : 年车库建成时间、车库面积、车库容量。 我们用0来填充缺失值 </li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">col</span> <span class="ow">in</span> <span class="p">(</span><span class="s1">&#39;GarageYrBlt&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageArea&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageCars&#39;</span><span class="p">):</span>
    <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>BsmtFinSF1, BsmtFinSF2, BsmtUnfSF, TotalBsmtSF, BsmtFullBath and BsmtHalfBath</strong> : 地下室相关属性，如果值缺失，就意味着没有地下室。填0</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">col</span> <span class="ow">in</span> <span class="p">(</span><span class="s1">&#39;BsmtFinSF1&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtFinSF2&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtUnfSF&#39;</span><span class="p">,</span><span class="s1">&#39;TotalBsmtSF&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtFullBath&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtHalfBath&#39;</span><span class="p">):</span>
    <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>BsmtQual, BsmtCond, BsmtExposure, BsmtFinType1 and BsmtFinType2</strong> : 地下室相关属性，如果值缺失，就意味着没有地下室。填None</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[23]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">for</span> <span class="n">col</span> <span class="ow">in</span> <span class="p">(</span><span class="s1">&#39;BsmtQual&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtCond&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtExposure&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtFinType1&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtFinType2&#39;</span><span class="p">):</span>
    <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="n">col</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s1">&#39;None&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>MasVnrArea and MasVnrType</strong> : 表层砌体面积和表层砌体类型。NA很可能意味着这些房屋没有砌筑饰面。我们可以给区域面积填充0和给类型填充None。 </li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;MasVnrType&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;MasVnrType&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
<span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;MasVnrArea&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;MasVnrArea&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>MSZoning (The general zoning classification)</strong> :  一共1460条数据，其中'RL' 出现了1151次。所以我们使用'RL'填充缺失值。</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MSZoning&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MSZoning&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MSZoning&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">mode</span><span class="p">()[</span><span class="mi">0</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Utilities</strong> : 这个属性中所有的值基本上都是"AllPub"，其中有1个"NoSeWa"和2个NA。而且'NoSewa'在训练集中出现了，在测试集中没有出现。<strong>因此该特征无助于预测建模</strong>。所有我们可以删掉它</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span> <span class="o">=</span> <span class="n">all_data</span><span class="o">.</span><span class="n">drop</span><span class="p">([</span><span class="s1">&#39;Utilities&#39;</span><span class="p">],</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Functional</strong> : 在说明文档中，数据缺失就意味着取值应该是"Typ"</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;Functional&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s2">&quot;Functional&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;Typ&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Electrical</strong> : 电气系统。只有一个缺失值，所以我们就用出现出现次数最多的值填充它。</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Electrical&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Electrical&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Electrical&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">mode</span><span class="p">()[</span><span class="mi">0</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>KitchenQual</strong>: 厨房的品质。和Electrical一样，只有一个缺失值，所以我们就用出现出现次数最多的值填充它。</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;KitchenQual&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;KitchenQual&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;KitchenQual&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">mode</span><span class="p">()[</span><span class="mi">0</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Exterior1st and Exterior2nd</strong> : 外墙面1、外墙面2.和上面一样</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Exterior1st&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Exterior1st&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Exterior1st&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">mode</span><span class="p">()[</span><span class="mi">0</span><span class="p">])</span>
<span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Exterior2nd&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Exterior2nd&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;Exterior2nd&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">mode</span><span class="p">()[</span><span class="mi">0</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>SaleType</strong> : 销售类型和上面一样</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;SaleType&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;SaleType&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;SaleType&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">mode</span><span class="p">()[</span><span class="mi">0</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>MSSubClass</strong> : 数据缺失可能表示它不是建筑类型。我们用None填充。</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MSSubClass&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MSSubClass&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们检查一下是否还有其他的缺失值</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#Check remaining missing values if any </span>
<span class="n">all_data_na</span> <span class="o">=</span> <span class="p">(</span><span class="n">all_data</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span> <span class="o">/</span> <span class="nb">len</span><span class="p">(</span><span class="n">all_data</span><span class="p">))</span> <span class="o">*</span> <span class="mi">100</span>
<span class="n">all_data_na</span> <span class="o">=</span> <span class="n">all_data_na</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">all_data_na</span><span class="p">[</span><span class="n">all_data_na</span> <span class="o">==</span> <span class="mi">0</span><span class="p">]</span><span class="o">.</span><span class="n">index</span><span class="p">)</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">missing_data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s1">&#39;Missing Ratio&#39;</span> <span class="p">:</span><span class="n">all_data_na</span><span class="p">})</span>
<span class="n">missing_data</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[33]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Missing Ratio</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>这意味着没有缺失值了。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#26356;&#22810;&#29305;&#24449;&#24037;&#31243;">&#26356;&#22810;&#29305;&#24449;&#24037;&#31243;<a class="anchor-link" href="#&#26356;&#22810;&#29305;&#24449;&#24037;&#31243;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>将一些数值型但是实际表示的是类型的特征做变换</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[34]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#MSSubClass=The building class</span>
<span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MSSubClass&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MSSubClass&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span>


<span class="c1">#Changing OverallCond into a categorical variable</span>
<span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;OverallCond&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;OverallCond&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span>


<span class="c1">#Year and month sold are transformed into categorical features.</span>
<span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;YrSold&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;YrSold&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span>
<span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MoSold&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;MoSold&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">astype</span><span class="p">(</span><span class="nb">str</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>LabelEncoder可以将标签分配一个0—n_classes-1之间的编码 
<strong>有些特征虽然表示种类，但是包含了顺序信息，使用LabelEncoder处理这些特征。</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="k">import</span> <span class="n">LabelEncoder</span>
<span class="n">cols</span> <span class="o">=</span> <span class="p">(</span><span class="s1">&#39;FireplaceQu&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtQual&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtCond&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageQual&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageCond&#39;</span><span class="p">,</span> 
        <span class="s1">&#39;ExterQual&#39;</span><span class="p">,</span> <span class="s1">&#39;ExterCond&#39;</span><span class="p">,</span><span class="s1">&#39;HeatingQC&#39;</span><span class="p">,</span> <span class="s1">&#39;PoolQC&#39;</span><span class="p">,</span> <span class="s1">&#39;KitchenQual&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtFinType1&#39;</span><span class="p">,</span> 
        <span class="s1">&#39;BsmtFinType2&#39;</span><span class="p">,</span> <span class="s1">&#39;Functional&#39;</span><span class="p">,</span> <span class="s1">&#39;Fence&#39;</span><span class="p">,</span> <span class="s1">&#39;BsmtExposure&#39;</span><span class="p">,</span> <span class="s1">&#39;GarageFinish&#39;</span><span class="p">,</span> <span class="s1">&#39;LandSlope&#39;</span><span class="p">,</span>
        <span class="s1">&#39;LotShape&#39;</span><span class="p">,</span> <span class="s1">&#39;PavedDrive&#39;</span><span class="p">,</span> <span class="s1">&#39;Street&#39;</span><span class="p">,</span> <span class="s1">&#39;Alley&#39;</span><span class="p">,</span> <span class="s1">&#39;CentralAir&#39;</span><span class="p">,</span> <span class="s1">&#39;MSSubClass&#39;</span><span class="p">,</span> <span class="s1">&#39;OverallCond&#39;</span><span class="p">,</span> 
        <span class="s1">&#39;YrSold&#39;</span><span class="p">,</span> <span class="s1">&#39;MoSold&#39;</span><span class="p">)</span>
<span class="c1"># process columns, apply LabelEncoder to categorical features</span>
<span class="k">for</span> <span class="n">c</span> <span class="ow">in</span> <span class="n">cols</span><span class="p">:</span>
    <span class="n">lbl</span> <span class="o">=</span> <span class="n">LabelEncoder</span><span class="p">()</span> 
    <span class="n">lbl</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="n">c</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">))</span> 
    <span class="n">all_data</span><span class="p">[</span><span class="n">c</span><span class="p">]</span> <span class="o">=</span> <span class="n">lbl</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="n">c</span><span class="p">]</span><span class="o">.</span><span class="n">values</span><span class="p">))</span>

<span class="c1"># shape        </span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Shape all_data: </span><span class="si">{}</span><span class="s1">&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">all_data</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Shape all_data: (2917, 78)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>增加一个重要的特征</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>由于面积相关特征对于确定房价非常重要，我们还增加了一个特征，即每个房屋的地下室总面积加一楼和二楼面积</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Adding total sqfootage feature </span>
<span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;TotalSF&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;TotalBsmtSF&#39;</span><span class="p">]</span> <span class="o">+</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;1stFlrSF&#39;</span><span class="p">]</span> <span class="o">+</span> <span class="n">all_data</span><span class="p">[</span><span class="s1">&#39;2ndFlrSF&#39;</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>倾斜的特征（非正态分布的特征）</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">numeric_feats</span> <span class="o">=</span> <span class="n">all_data</span><span class="o">.</span><span class="n">dtypes</span><span class="p">[</span><span class="n">all_data</span><span class="o">.</span><span class="n">dtypes</span> <span class="o">!=</span> <span class="s2">&quot;object&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">index</span>

<span class="c1"># Check the skew of all numerical features</span>
<span class="n">skewed_feats</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="n">numeric_feats</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">skew</span><span class="p">(</span><span class="n">x</span><span class="o">.</span><span class="n">dropna</span><span class="p">()))</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">ascending</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">Skew in numerical features: </span><span class="se">\n</span><span class="s2">&quot;</span><span class="p">)</span>
<span class="n">skewness</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s1">&#39;Skew&#39;</span> <span class="p">:</span><span class="n">skewed_feats</span><span class="p">})</span>
<span class="n">skewness</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>
Skew in numerical features: 

</pre>
</div>
</div>

<div class="output_area">

<div class="prompt output_prompt">Out[37]:</div>



<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Skew</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>MiscVal</th>
      <td>21.940</td>
    </tr>
    <tr>
      <th>PoolArea</th>
      <td>17.689</td>
    </tr>
    <tr>
      <th>LotArea</th>
      <td>13.109</td>
    </tr>
    <tr>
      <th>LowQualFinSF</th>
      <td>12.085</td>
    </tr>
    <tr>
      <th>3SsnPorch</th>
      <td>11.372</td>
    </tr>
    <tr>
      <th>LandSlope</th>
      <td>4.973</td>
    </tr>
    <tr>
      <th>KitchenAbvGr</th>
      <td>4.301</td>
    </tr>
    <tr>
      <th>BsmtFinSF2</th>
      <td>4.145</td>
    </tr>
    <tr>
      <th>EnclosedPorch</th>
      <td>4.002</td>
    </tr>
    <tr>
      <th>ScreenPorch</th>
      <td>3.945</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>对（十分）倾斜特征做Box-Cox变换</strong></p>
<p>Box-Cox变换是Box和Cox在1964年提出的一种广义幂变换方法，是统计建模中常用的一种数据变换，用于连续的响应变量不满足正态分布的情况。Box-Cox变换之后，可以一定程度上减小不可观测的误差和预测变量的相关性。Box-Cox变换的主要特点是引入一个参数，通过数据本身估计该参数进而确定应采取的数据变换形式，Box-Cox变换可以明显地改善数据的正态性、对称性和方差相等性，对许多实际数据都是行之有效的</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们使用scipy中的boxcox1p函数，它可以计算<strong>$1 + x$</strong>的Box-Cox变换</p>

<pre><code>y = ((1+x)**lmbda - 1) / lmbda  if lmbda != 0
    log(1+x)             if lmbda == 0</code></pre>
<p>从上面的公式我们可以看出，当 $ \lambda = 0 $ 时，它和我们上面对目标变量做的对数变换一样。</p>
<p>我们可以从下面两个页面中知道更多关于Box-Cox变换的细节<a href="http://onlinestatbook.com/2/transformations/box-cox.html">this page</a> and  <a href="https://docs.scipy.org/doc/scipy-0.19.0/reference/generated/scipy.special.boxcox1p.html">the scipy function's page</a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">skewness</span> <span class="o">=</span> <span class="n">skewness</span><span class="p">[</span><span class="nb">abs</span><span class="p">(</span><span class="n">skewness</span><span class="p">)</span> <span class="o">&gt;</span> <span class="mf">0.75</span><span class="p">]</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;There are </span><span class="si">{}</span><span class="s2"> skewed numerical features to Box Cox transform&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">skewness</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]))</span>

<span class="kn">from</span> <span class="nn">scipy.special</span> <span class="k">import</span> <span class="n">boxcox1p</span>
<span class="n">skewed_features</span> <span class="o">=</span> <span class="n">skewness</span><span class="o">.</span><span class="n">index</span>
<span class="n">lam</span> <span class="o">=</span> <span class="mf">0.15</span>
<span class="k">for</span> <span class="n">feat</span> <span class="ow">in</span> <span class="n">skewed_features</span><span class="p">:</span>
    <span class="c1">#all_data[feat] += 1</span>
    <span class="n">all_data</span><span class="p">[</span><span class="n">feat</span><span class="p">]</span> <span class="o">=</span> <span class="n">boxcox1p</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="n">feat</span><span class="p">],</span> <span class="n">lam</span><span class="p">)</span>
    
<span class="c1">#all_data[skewed_features] = np.log1p(all_data[skewed_features])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>There are 59 skewed numerical features to Box Cox transform
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>对哑变量编码</strong></p>
<p>pandas使用get_dummies进行one-hot编码</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[39]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">get_dummies</span><span class="p">(</span><span class="n">all_data</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">all_data</span><span class="o">.</span><span class="n">shape</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>(2917, 220)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>获取新的训练集和测试集</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">train</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[:</span><span class="n">ntrain</span><span class="p">]</span>
<span class="n">test</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="n">ntrain</span><span class="p">:]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="&#35757;&#32451;&#27169;&#22411;">&#35757;&#32451;&#27169;&#22411;<a class="anchor-link" href="#&#35757;&#32451;&#27169;&#22411;">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>引入依赖库</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[41]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">ElasticNet</span><span class="p">,</span> <span class="n">Lasso</span><span class="p">,</span>  <span class="n">BayesianRidge</span><span class="p">,</span> <span class="n">LassoLarsIC</span>
<span class="kn">from</span> <span class="nn">sklearn.ensemble</span> <span class="k">import</span> <span class="n">RandomForestRegressor</span><span class="p">,</span>  <span class="n">GradientBoostingRegressor</span>
<span class="kn">from</span> <span class="nn">sklearn.kernel_ridge</span> <span class="k">import</span> <span class="n">KernelRidge</span>
<span class="kn">from</span> <span class="nn">sklearn.pipeline</span> <span class="k">import</span> <span class="n">make_pipeline</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="k">import</span> <span class="n">RobustScaler</span>
<span class="kn">from</span> <span class="nn">sklearn.base</span> <span class="k">import</span> <span class="n">BaseEstimator</span><span class="p">,</span> <span class="n">TransformerMixin</span><span class="p">,</span> <span class="n">RegressorMixin</span><span class="p">,</span> <span class="n">clone</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">KFold</span><span class="p">,</span> <span class="n">cross_val_score</span><span class="p">,</span> <span class="n">train_test_split</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">mean_squared_error</span>
<span class="kn">import</span> <span class="nn">xgboost</span> <span class="k">as</span> <span class="nn">xgb</span>
<span class="kn">import</span> <span class="nn">lightgbm</span> <span class="k">as</span> <span class="nn">lgb</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>定义一个交叉验证的策略</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>由于这个函数没有考虑随机性，所以我们在这自强增加一行代码，在交叉验证之前把数据打乱
我们使用Sklearn的<strong>cross_val_score</strong>来做K折交叉验证。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[42]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#Validation function</span>
<span class="n">n_folds</span> <span class="o">=</span> <span class="mi">5</span>

<span class="k">def</span> <span class="nf">rmsle_cv</span><span class="p">(</span><span class="n">model</span><span class="p">):</span>
    <span class="n">kf</span> <span class="o">=</span> <span class="n">KFold</span><span class="p">(</span><span class="n">n_folds</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span><span class="o">.</span><span class="n">get_n_splits</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">values</span><span class="p">)</span>
    <span class="n">rmse</span><span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="o">-</span><span class="n">cross_val_score</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">train</span><span class="o">.</span><span class="n">values</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">scoring</span><span class="o">=</span><span class="s2">&quot;neg_mean_squared_error&quot;</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="n">kf</span><span class="p">))</span>
    <span class="k">return</span><span class="p">(</span><span class="n">rmse</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="&#22522;&#30784;&#27169;&#22411;">&#22522;&#30784;&#27169;&#22411;<a class="anchor-link" href="#&#22522;&#30784;&#27169;&#22411;">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>LASSO  Regression</strong>  : L1范数正则化（Lasso回归）的线性回归</li>
</ul>
<p>该模型可能对异常值非常敏感。 所以我们需要让它们更加健壮。所以我们对pipeline使用sklearn的<strong>Robustscaler()</strong>方法</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[43]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">lasso</span> <span class="o">=</span> <span class="n">make_pipeline</span><span class="p">(</span><span class="n">RobustScaler</span><span class="p">(),</span> <span class="n">Lasso</span><span class="p">(</span><span class="n">alpha</span> <span class="o">=</span><span class="mf">0.0005</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">1</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Elastic Net Regression</strong> : L1和L2正则化的线性回归</li>
</ul>
<p>同上</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[44]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">ENet</span> <span class="o">=</span> <span class="n">make_pipeline</span><span class="p">(</span><span class="n">RobustScaler</span><span class="p">(),</span> <span class="n">ElasticNet</span><span class="p">(</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.0005</span><span class="p">,</span> <span class="n">l1_ratio</span><span class="o">=.</span><span class="mi">9</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">3</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Kernel Ridge Regression</strong> :L2正则线性回归</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[45]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">KRR</span> <span class="o">=</span> <span class="n">KernelRidge</span><span class="p">(</span><span class="n">alpha</span><span class="o">=</span><span class="mf">0.6</span><span class="p">,</span> <span class="n">kernel</span><span class="o">=</span><span class="s1">&#39;polynomial&#39;</span><span class="p">,</span> <span class="n">degree</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">coef0</span><span class="o">=</span><span class="mf">2.5</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>Gradient Boosting Regression</strong> :背景梯度提升回归</li>
</ul>
<p>为了使程序更健壮，我们使用<strong>huber</strong> loss</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[46]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">GBoost</span> <span class="o">=</span> <span class="n">GradientBoostingRegressor</span><span class="p">(</span><span class="n">n_estimators</span><span class="o">=</span><span class="mi">3000</span><span class="p">,</span> <span class="n">learning_rate</span><span class="o">=</span><span class="mf">0.05</span><span class="p">,</span>
                                   <span class="n">max_depth</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">max_features</span><span class="o">=</span><span class="s1">&#39;sqrt&#39;</span><span class="p">,</span>
                                   <span class="n">min_samples_leaf</span><span class="o">=</span><span class="mi">15</span><span class="p">,</span> <span class="n">min_samples_split</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> 
                                   <span class="n">loss</span><span class="o">=</span><span class="s1">&#39;huber&#39;</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span><span class="mi">5</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>XGBoost</strong> :</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[47]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_xgb</span> <span class="o">=</span> <span class="n">xgb</span><span class="o">.</span><span class="n">XGBRegressor</span><span class="p">(</span><span class="n">colsample_bytree</span><span class="o">=</span><span class="mf">0.4603</span><span class="p">,</span> <span class="n">gamma</span><span class="o">=</span><span class="mf">0.0468</span><span class="p">,</span> 
                             <span class="n">learning_rate</span><span class="o">=</span><span class="mf">0.05</span><span class="p">,</span> <span class="n">max_depth</span><span class="o">=</span><span class="mi">3</span><span class="p">,</span> 
                             <span class="n">min_child_weight</span><span class="o">=</span><span class="mf">1.7817</span><span class="p">,</span> <span class="n">n_estimators</span><span class="o">=</span><span class="mi">2200</span><span class="p">,</span>
                             <span class="n">reg_alpha</span><span class="o">=</span><span class="mf">0.4640</span><span class="p">,</span> <span class="n">reg_lambda</span><span class="o">=</span><span class="mf">0.8571</span><span class="p">,</span>
                             <span class="n">subsample</span><span class="o">=</span><span class="mf">0.5213</span><span class="p">,</span> <span class="n">silent</span><span class="o">=</span><span class="mi">1</span><span class="p">,</span>
                             <span class="n">random_state</span> <span class="o">=</span><span class="mi">7</span><span class="p">,</span> <span class="n">nthread</span> <span class="o">=</span> <span class="o">-</span><span class="mi">1</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<ul>
<li><strong>LightGBM</strong> :</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[48]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_lgb</span> <span class="o">=</span> <span class="n">lgb</span><span class="o">.</span><span class="n">LGBMRegressor</span><span class="p">(</span><span class="n">objective</span><span class="o">=</span><span class="s1">&#39;regression&#39;</span><span class="p">,</span><span class="n">num_leaves</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span>
                              <span class="n">learning_rate</span><span class="o">=</span><span class="mf">0.05</span><span class="p">,</span> <span class="n">n_estimators</span><span class="o">=</span><span class="mi">720</span><span class="p">,</span>
                              <span class="n">max_bin</span> <span class="o">=</span> <span class="mi">55</span><span class="p">,</span> <span class="n">bagging_fraction</span> <span class="o">=</span> <span class="mf">0.8</span><span class="p">,</span>
                              <span class="n">bagging_freq</span> <span class="o">=</span> <span class="mi">5</span><span class="p">,</span> <span class="n">feature_fraction</span> <span class="o">=</span> <span class="mf">0.2319</span><span class="p">,</span>
                              <span class="n">feature_fraction_seed</span><span class="o">=</span><span class="mi">9</span><span class="p">,</span> <span class="n">bagging_seed</span><span class="o">=</span><span class="mi">9</span><span class="p">,</span>
                              <span class="n">min_data_in_leaf</span> <span class="o">=</span><span class="mi">6</span><span class="p">,</span> <span class="n">min_sum_hessian_in_leaf</span> <span class="o">=</span> <span class="mi">11</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#22522;&#30784;&#27169;&#22411;&#35780;&#20998;">&#22522;&#30784;&#27169;&#22411;&#35780;&#20998;<a class="anchor-link" href="#&#22522;&#30784;&#27169;&#22411;&#35780;&#20998;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>让我们通过评估交叉验证的rmsle来了解这些基本模型的运行表现</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[49]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">lasso</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;</span><span class="se">\n</span><span class="s2">Lasso score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>
Lasso score: 0.1115 (0.0074)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[50]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">ENet</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;ElasticNet score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>ElasticNet score: 0.1116 (0.0074)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[51]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">KRR</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Kernel Ridge score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Kernel Ridge score: 0.1153 (0.0075)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[52]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">GBoost</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Gradient Boosting score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Gradient Boosting score: 0.1177 (0.0080)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[53]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">model_xgb</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Xgboost score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Xgboost score: 0.1165 (0.0054)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[54]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">model_lgb</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;LGBM score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span> <span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>LGBM score: 0.1162 (0.0071)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Stacking--models">Stacking  models<a class="anchor-link" href="#Stacking--models">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#26368;&#31616;&#21333;&#30340;Stacking&#27169;&#22411;&#25506;&#32034;&#65306;&#22522;&#30784;&#27169;&#22411;&#24179;&#22343;">&#26368;&#31616;&#21333;&#30340;Stacking&#27169;&#22411;&#25506;&#32034;&#65306;&#22522;&#30784;&#27169;&#22411;&#24179;&#22343;<a class="anchor-link" href="#&#26368;&#31616;&#21333;&#30340;Stacking&#27169;&#22411;&#25506;&#32034;&#65306;&#22522;&#30784;&#27169;&#22411;&#24179;&#22343;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们从这种平均基本模型的简单方法开始。 我们构建了一个新类来扩展scikit-learn与我们的模型，并且还包括封装和代码重用(<a href="https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)">inheritance</a>)</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Averaged base models class</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[55]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">AveragingModels</span><span class="p">(</span><span class="n">BaseEstimator</span><span class="p">,</span> <span class="n">RegressorMixin</span><span class="p">,</span> <span class="n">TransformerMixin</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">models</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">models</span> <span class="o">=</span> <span class="n">models</span>
        
    <span class="c1"># we define clones of the original models to fit the data in</span>
    <span class="k">def</span> <span class="nf">fit</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">models_</span> <span class="o">=</span> <span class="p">[</span><span class="n">clone</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="k">for</span> <span class="n">x</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">models</span><span class="p">]</span>
        
        <span class="c1"># Train cloned base models</span>
        <span class="k">for</span> <span class="n">model</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">models_</span><span class="p">:</span>
            <span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>

        <span class="k">return</span> <span class="bp">self</span>
    
    <span class="c1">#Now we do the predictions for cloned models and average them</span>
    <span class="k">def</span> <span class="nf">predict</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">):</span>
        <span class="n">predictions</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">column_stack</span><span class="p">([</span>
            <span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X</span><span class="p">)</span> <span class="k">for</span> <span class="n">model</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">models_</span>
        <span class="p">])</span>
        <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">predictions</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>   
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Averaged base models score</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们只使用 <strong>ENet, GBoost,  KRR and lasso</strong>这四个模型做平均。当然，我们可以轻松的增加模型。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[56]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">averaged_models</span> <span class="o">=</span> <span class="n">AveragingModels</span><span class="p">(</span><span class="n">models</span> <span class="o">=</span> <span class="p">(</span><span class="n">ENet</span><span class="p">,</span> <span class="n">GBoost</span><span class="p">,</span> <span class="n">KRR</span><span class="p">,</span> <span class="n">lasso</span><span class="p">))</span>

<span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">averaged_models</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot; Averaged base models score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)</span><span class="se">\n</span><span class="s2">&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre> Averaged base models score: 0.1091 (0.0075)

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>哇 ！ 似乎最简单的Stacking模型确实提高了分数。 这鼓励了我们要进一步探索一个不那么简单的堆叠方法。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#19981;&#22826;&#31616;&#21333;&#30340;Stacking&#27169;&#22411;&#65306;&#22686;&#21152;&#19968;&#20010;&#20803;&#27169;&#22411;&#65288;Meta-model&#65289;">&#19981;&#22826;&#31616;&#21333;&#30340;Stacking&#27169;&#22411;&#65306;&#22686;&#21152;&#19968;&#20010;&#20803;&#27169;&#22411;&#65288;Meta-model&#65289;<a class="anchor-link" href="#&#19981;&#22826;&#31616;&#21333;&#30340;Stacking&#27169;&#22411;&#65306;&#22686;&#21152;&#19968;&#20010;&#20803;&#27169;&#22411;&#65288;Meta-model&#65289;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>在这种方法中，我们在平均基础模型上增加一个元模型，用这些基本模型的剩余的一折的预测值来训练我们的元模型</p>
<p>训练部分的程序符合下面的描述：</p>
<ol>
<li><p>将整个训练集分成两个不相交的集（这里是<strong>train</strong>和.<strong>holdout</strong>）</p>
</li>
<li><p>在第一部分（<strong>train</strong>）数据上训练几个基础模型</p>
</li>
<li><p>在第二部分（<strong>holdout</strong>）数据上测试（预测、打分）这些基础模型</p>
</li>
<li><p>使用来自3）的预测(称为out-of-folds predictions) 作为输入, and the correct responses (目标变量) 作为输出来训练更高级别的学习器称为<strong>元模型meta-model</strong>.</p>
</li>
</ol>
<p>前三个步骤是迭代完成的。如果我们使用5折举例子，我们首先将训练数据分成5份。然后我们将进行5次迭代。在每次迭代中，我们使用4份数据训练基础模型，然后预测剩下的一份数据(holdout fold)。</p>
<p>因此，经过5次迭代后，整个数据集都被循环预测了，在第四步，我们使用它作为新的特征来训练我们的元模型。</p>
<p>对于预测部分，我们对测试数据上所有基础模型的预测进行平均，并将它们用作元特征<strong>meta-features</strong>，最终预测是使用元模型完成的。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><img src="http://i.imgur.com/QBuDOjs.jpg" alt="Faron"></p>
<p>(Image taken from <a href="https://www.kaggle.com/getting-started/18153#post103381">Faron</a>)</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><img src="http://s5047.pcdn.co/wp-content/uploads/2017/06/image5.gif" alt="kaz"></p>
<p>Gif taken from <a href="http://blog.kaggle.com/2017/06/15/stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/">KazAnova's interview</a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>在这个gif上，基本模型是算法0,1,2，元模型是算法3.整个训练数据集是A + B（目标变量y已知），我们可以分成训练部分（A）和holdout部分（B）。 测试数据集是C.</p>
<p>B1（来自holdout部分的预测值）是用于训练元模型3的新特征，并且C1（其是来自测试数据集的预测）是完成最终预测的元特征。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Stacking averaged Models Class</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[57]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">StackingAveragedModels</span><span class="p">(</span><span class="n">BaseEstimator</span><span class="p">,</span> <span class="n">RegressorMixin</span><span class="p">,</span> <span class="n">TransformerMixin</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">base_models</span><span class="p">,</span> <span class="n">meta_model</span><span class="p">,</span> <span class="n">n_folds</span><span class="o">=</span><span class="mi">5</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">base_models</span> <span class="o">=</span> <span class="n">base_models</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">meta_model</span> <span class="o">=</span> <span class="n">meta_model</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">n_folds</span> <span class="o">=</span> <span class="n">n_folds</span>
   
    <span class="c1"># We again fit the data on clones of the original models</span>
    <span class="k">def</span> <span class="nf">fit</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">):</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">base_models_</span> <span class="o">=</span> <span class="p">[</span><span class="nb">list</span><span class="p">()</span> <span class="k">for</span> <span class="n">x</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">base_models</span><span class="p">]</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">meta_model_</span> <span class="o">=</span> <span class="n">clone</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">meta_model</span><span class="p">)</span>
        <span class="n">kfold</span> <span class="o">=</span> <span class="n">KFold</span><span class="p">(</span><span class="n">n_splits</span><span class="o">=</span><span class="bp">self</span><span class="o">.</span><span class="n">n_folds</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">156</span><span class="p">)</span>
        
        <span class="c1"># Train cloned base models then create out-of-fold predictions</span>
        <span class="c1"># that are needed to train the cloned meta-model</span>
        <span class="n">out_of_fold_predictions</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">((</span><span class="n">X</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="nb">len</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">base_models</span><span class="p">)))</span>
        <span class="k">for</span> <span class="n">i</span><span class="p">,</span> <span class="n">model</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">base_models</span><span class="p">):</span>
            <span class="k">for</span> <span class="n">train_index</span><span class="p">,</span> <span class="n">holdout_index</span> <span class="ow">in</span> <span class="n">kfold</span><span class="o">.</span><span class="n">split</span><span class="p">(</span><span class="n">X</span><span class="p">,</span> <span class="n">y</span><span class="p">):</span>
                <span class="n">instance</span> <span class="o">=</span> <span class="n">clone</span><span class="p">(</span><span class="n">model</span><span class="p">)</span>
                <span class="bp">self</span><span class="o">.</span><span class="n">base_models_</span><span class="p">[</span><span class="n">i</span><span class="p">]</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">instance</span><span class="p">)</span>
                <span class="n">instance</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X</span><span class="p">[</span><span class="n">train_index</span><span class="p">],</span> <span class="n">y</span><span class="p">[</span><span class="n">train_index</span><span class="p">])</span>
                <span class="n">y_pred</span> <span class="o">=</span> <span class="n">instance</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X</span><span class="p">[</span><span class="n">holdout_index</span><span class="p">])</span>
                <span class="n">out_of_fold_predictions</span><span class="p">[</span><span class="n">holdout_index</span><span class="p">,</span> <span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">y_pred</span>
                
        <span class="c1"># Now train the cloned  meta-model using the out-of-fold predictions as new feature</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">meta_model_</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">out_of_fold_predictions</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
        <span class="k">return</span> <span class="bp">self</span>
   
    <span class="c1">#Do the predictions of all base models on the test data and use the averaged predictions as </span>
    <span class="c1">#meta-features for the final prediction which is done by the meta-model</span>
    <span class="k">def</span> <span class="nf">predict</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">X</span><span class="p">):</span>
        <span class="n">meta_features</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">column_stack</span><span class="p">([</span>
            <span class="n">np</span><span class="o">.</span><span class="n">column_stack</span><span class="p">([</span><span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X</span><span class="p">)</span> <span class="k">for</span> <span class="n">model</span> <span class="ow">in</span> <span class="n">base_models</span><span class="p">])</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">axis</span><span class="o">=</span><span class="mi">1</span><span class="p">)</span>
            <span class="k">for</span> <span class="n">base_models</span> <span class="ow">in</span> <span class="bp">self</span><span class="o">.</span><span class="n">base_models_</span> <span class="p">])</span>
        <span class="k">return</span> <span class="bp">self</span><span class="o">.</span><span class="n">meta_model_</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">meta_features</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Stacking Averaged models Score</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>To make the two approaches comparable (by using the same number of models) , we just average <strong>Enet KRR and Gboost</strong>, then we add <strong>lasso as meta-model</strong>.
为了使两种方法具有可比性（通过使用相同数量的模型），我们使用<strong>Enet KRR 和 Gboost</strong>作为基础模型，增加<strong>lasso</strong>作为元模型。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[58]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">stacked_averaged_models</span> <span class="o">=</span> <span class="n">StackingAveragedModels</span><span class="p">(</span><span class="n">base_models</span> <span class="o">=</span> <span class="p">(</span><span class="n">ENet</span><span class="p">,</span> <span class="n">GBoost</span><span class="p">,</span> <span class="n">KRR</span><span class="p">),</span>
                                                 <span class="n">meta_model</span> <span class="o">=</span> <span class="n">lasso</span><span class="p">)</span>

<span class="n">score</span> <span class="o">=</span> <span class="n">rmsle_cv</span><span class="p">(</span><span class="n">stacked_averaged_models</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Stacking Averaged models score: </span><span class="si">{:.4f}</span><span class="s2"> (</span><span class="si">{:.4f}</span><span class="s2">)&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">score</span><span class="o">.</span><span class="n">mean</span><span class="p">(),</span> <span class="n">score</span><span class="o">.</span><span class="n">std</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Stacking Averaged models score: 0.1085 (0.0074)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>通过添加元学习器，我们再次获得更好的分数</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="&#38598;&#25104;-StackedRegressor,-XGBoost-&#21644;-LightGBM">&#38598;&#25104; StackedRegressor, XGBoost &#21644; LightGBM<a class="anchor-link" href="#&#38598;&#25104;-StackedRegressor,-XGBoost-&#21644;-LightGBM">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们增加 <strong>XGBoost and LightGBM</strong>到前面定义的<strong>StackedRegressor</strong>上。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们首先定义一个rmsle评估函数</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[59]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">def</span> <span class="nf">rmsle</span><span class="p">(</span><span class="n">y</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">):</span>
    <span class="k">return</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">mean_squared_error</span><span class="p">(</span><span class="n">y</span><span class="p">,</span> <span class="n">y_pred</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#26368;&#32456;&#30340;&#35757;&#32451;&#19982;&#39044;&#27979;">&#26368;&#32456;&#30340;&#35757;&#32451;&#19982;&#39044;&#27979;<a class="anchor-link" href="#&#26368;&#32456;&#30340;&#35757;&#32451;&#19982;&#39044;&#27979;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>StackedRegressor:</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[60]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">stacked_averaged_models</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">values</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">stacked_train_pred</span> <span class="o">=</span> <span class="n">stacked_averaged_models</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">values</span><span class="p">)</span>
<span class="n">stacked_pred</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">expm1</span><span class="p">(</span><span class="n">stacked_averaged_models</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">test</span><span class="o">.</span><span class="n">values</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="n">rmsle</span><span class="p">(</span><span class="n">y_train</span><span class="p">,</span> <span class="n">stacked_train_pred</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>0.07815719379164107
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>XGBoost:</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[61]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_xgb</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">xgb_train_pred</span> <span class="o">=</span> <span class="n">model_xgb</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">train</span><span class="p">)</span>
<span class="n">xgb_pred</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">expm1</span><span class="p">(</span><span class="n">model_xgb</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">test</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="n">rmsle</span><span class="p">(</span><span class="n">y_train</span><span class="p">,</span> <span class="n">xgb_train_pred</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>0.0815823282299117
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>LightGBM:</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[62]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_lgb</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">lgb_train_pred</span> <span class="o">=</span> <span class="n">model_lgb</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">train</span><span class="p">)</span>
<span class="n">lgb_pred</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">expm1</span><span class="p">(</span><span class="n">model_lgb</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">test</span><span class="o">.</span><span class="n">values</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="n">rmsle</span><span class="p">(</span><span class="n">y_train</span><span class="p">,</span> <span class="n">lgb_train_pred</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>0.07307464036005418
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[63]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="sd">&#39;&#39;&#39;RMSE on the entire Train data when averaging&#39;&#39;&#39;</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;RMSLE score on train data:&#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">rmsle</span><span class="p">(</span><span class="n">y_train</span><span class="p">,</span><span class="n">stacked_train_pred</span><span class="o">*</span><span class="mf">0.70</span> <span class="o">+</span>
               <span class="n">xgb_train_pred</span><span class="o">*</span><span class="mf">0.15</span> <span class="o">+</span> <span class="n">lgb_train_pred</span><span class="o">*</span><span class="mf">0.15</span> <span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>RMSLE score on train data:
0.07586557397142984
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Ensemble prediction:</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[64]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">ensemble</span> <span class="o">=</span> <span class="n">stacked_pred</span><span class="o">*</span><span class="mf">0.70</span> <span class="o">+</span> <span class="n">xgb_pred</span><span class="o">*</span><span class="mf">0.15</span> <span class="o">+</span> <span class="n">lgb_pred</span><span class="o">*</span><span class="mf">0.15</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><strong>Submission</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[65]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">sub</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">()</span>
<span class="n">sub</span><span class="p">[</span><span class="s1">&#39;Id&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">test_ID</span>
<span class="n">sub</span><span class="p">[</span><span class="s1">&#39;SalePrice&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">ensemble</span>
<span class="n">sub</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s1">&#39;submission.csv&#39;</span><span class="p">,</span><span class="n">index</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>
