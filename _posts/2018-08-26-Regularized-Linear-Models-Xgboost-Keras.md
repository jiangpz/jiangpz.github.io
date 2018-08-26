---
layout: post
title:  "Regularized Linear Models, Xgboost And Feedforward Neural Nets"
excerpt: "Kaggle House Prices 使用线性回归、xgboost和前馈神经网络预测房价"
date:   2018-08-26 07:01:08 +0800
categories: Kaggle
tags: [Kaggle, Modeling, xgboost]
comments: true
---

<html>
<head><meta charset="utf-8" />
<title>Regularized-Linear-Models-Xgboost-Keras</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
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
<p>原链接：<a href="https://www.kaggle.com/apapiu/regularized-linear-models">https://www.kaggle.com/apapiu/regularized-linear-models</a></p>
<h2 id="&#32447;&#24615;&#27169;&#22411;:">&#32447;&#24615;&#27169;&#22411;:<a class="anchor-link" href="#&#32447;&#24615;&#27169;&#22411;:">&#182;</a></h2><p>作者: Alexandru Papiu (<a href="https://twitter.com/apapiu">@apapiu</a>, <a href="https://github.com/apapiu">GitHub</a>)</p>
<p>There have been a few <a href="https://www.kaggle.com/comartel/house-prices-advanced-regression-techniques/house-price-xgboost-starter/run/348739">great</a>  <a href="https://www.kaggle.com/zoupet/house-prices-advanced-regression-techniques/xgboost-10-kfolds-with-scikit-learn/run/357561">scripts</a> on <a href="https://www.kaggle.com/tadepalli/house-prices-advanced-regression-techniques/xgboost-with-n-trees-autostop-0-12638/run/353049">xgboost</a> already so I'd figured I'd try something simpler: a regularized linear regression model. 现在已经有一些很棒的xgboost的脚本了，但是我想尝试一些简单的模型：一个正则化的线性回归模型。令人惊讶的是，虽然特征很少，但是它很有用。关键是要对数字变量进行对数变换，因为它们中的大多数的分布都是偏斜的。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">import</span> <span class="nn">matplotlib</span>

<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">from</span> <span class="nn">scipy.stats</span> <span class="k">import</span> <span class="n">skew</span>
<span class="kn">from</span> <span class="nn">scipy.stats.stats</span> <span class="k">import</span> <span class="n">pearsonr</span>


<span class="o">%</span><span class="k">config</span> InlineBackend.figure_format = &#39;retina&#39; #set &#39;png&#39; here when working on notebook
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">train</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s2">&quot;input/train.csv&quot;</span><span class="p">)</span>
<span class="n">test</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s2">&quot;input/test.csv&quot;</span><span class="p">)</span>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">train</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
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
      <td>65.0</td>
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
      <td>80.0</td>
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
      <td>68.0</td>
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
      <td>60.0</td>
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
      <td>84.0</td>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">((</span><span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span><span class="s1">&#39;MSSubClass&#39;</span><span class="p">:</span><span class="s1">&#39;SaleCondition&#39;</span><span class="p">],</span>
                      <span class="n">test</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span><span class="s1">&#39;MSSubClass&#39;</span><span class="p">:</span><span class="s1">&#39;SaleCondition&#39;</span><span class="p">]))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#25968;&#25454;&#39044;&#22788;&#29702;:">&#25968;&#25454;&#39044;&#22788;&#29702;:<a class="anchor-link" href="#&#25968;&#25454;&#39044;&#22788;&#29702;:">&#182;</a></h3><p>我们在这里不做任何猜想:</p>
<ul>
<li>首先，我们做对数变换，将特征变为正态分布    </li>
<li>为哑变量创建虚拟变量    </li>
<li>将数字缺失值（NaN）替换为各自列的平均值</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">matplotlib</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;figure.figsize&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mf">12.0</span><span class="p">,</span> <span class="mf">6.0</span><span class="p">)</span>
<span class="n">prices</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s2">&quot;price&quot;</span><span class="p">:</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">],</span> <span class="s2">&quot;log(price + 1)&quot;</span><span class="p">:</span><span class="n">np</span><span class="o">.</span><span class="n">log1p</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">])})</span>
<span class="n">prices</span><span class="o">.</span><span class="n">hist</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[5]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>array([[&lt;matplotlib.axes._subplots.AxesSubplot object at 0x0000023C846D16D8&gt;,
        &lt;matplotlib.axes._subplots.AxesSubplot object at 0x0000023C846482B0&gt;]],
      dtype=object)</pre>
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
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#log transform the target:</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">log1p</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">])</span>

<span class="c1">#log transform skewed numeric features:</span>
<span class="n">numeric_feats</span> <span class="o">=</span> <span class="n">all_data</span><span class="o">.</span><span class="n">dtypes</span><span class="p">[</span><span class="n">all_data</span><span class="o">.</span><span class="n">dtypes</span> <span class="o">!=</span> <span class="s2">&quot;object&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">index</span>

<span class="n">skewed_feats</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="n">numeric_feats</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">skew</span><span class="p">(</span><span class="n">x</span><span class="o">.</span><span class="n">dropna</span><span class="p">()))</span> <span class="c1">#compute skewness</span>
<span class="n">skewed_feats</span> <span class="o">=</span> <span class="n">skewed_feats</span><span class="p">[</span><span class="n">skewed_feats</span> <span class="o">&gt;</span> <span class="mf">0.75</span><span class="p">]</span>
<span class="n">skewed_feats</span> <span class="o">=</span> <span class="n">skewed_feats</span><span class="o">.</span><span class="n">index</span>

<span class="n">all_data</span><span class="p">[</span><span class="n">skewed_feats</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">log1p</span><span class="p">(</span><span class="n">all_data</span><span class="p">[</span><span class="n">skewed_feats</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stderr output_text">
<pre>C:\Python\Anaconda3\lib\site-packages\ipykernel_launcher.py:11: RuntimeWarning: invalid value encountered in log1p
  # This is added back by InteractiveShellApp.init_path()
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">all_data</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">get_dummies</span><span class="p">(</span><span class="n">all_data</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#filling NA&#39;s with the mean of the column:</span>
<span class="n">all_data</span> <span class="o">=</span> <span class="n">all_data</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">all_data</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#creating matrices for sklearn:</span>
<span class="n">X_train</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[:</span><span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]]</span>
<span class="n">X_test</span> <span class="o">=</span> <span class="n">all_data</span><span class="p">[</span><span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]:]</span>
<span class="n">y</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">SalePrice</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#35757;&#32451;&#27169;&#22411;">&#35757;&#32451;&#27169;&#22411;<a class="anchor-link" href="#&#35757;&#32451;&#27169;&#22411;">&#182;</a></h3><p>现在我们将使用scikit学习模块中的正则化线性回归模型。 我将尝试l_1（Lasso）和l_2（Ridge）正则化。 我还将定义一个返回交叉验证rmse错误的函数，以便我们可以评估我们的模型并选择最佳调整标准</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">Ridge</span><span class="p">,</span> <span class="n">RidgeCV</span><span class="p">,</span> <span class="n">ElasticNet</span><span class="p">,</span> <span class="n">LassoCV</span><span class="p">,</span> <span class="n">LassoLarsCV</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">cross_val_score</span>

<span class="k">def</span> <span class="nf">rmse_cv</span><span class="p">(</span><span class="n">model</span><span class="p">):</span>
    <span class="n">rmse</span><span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="o">-</span><span class="n">cross_val_score</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">X_train</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">scoring</span><span class="o">=</span><span class="s2">&quot;neg_mean_squared_error&quot;</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">5</span><span class="p">))</span>
    <span class="k">return</span><span class="p">(</span><span class="n">rmse</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_ridge</span> <span class="o">=</span> <span class="n">Ridge</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Ridge模型的主要调整参数是alpha - 一个正则化参数，用于衡量模型的灵活程度。 正规化越高，我们的模型就越不容易过度拟合。 但是它也会失去灵活性，并且可能无法捕获数据中的所有信号。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.05</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mf">0.3</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">15</span><span class="p">,</span> <span class="mi">30</span><span class="p">,</span> <span class="mi">50</span><span class="p">,</span> <span class="mi">75</span><span class="p">]</span>
<span class="n">cv_ridge</span> <span class="o">=</span> <span class="p">[</span><span class="n">rmse_cv</span><span class="p">(</span><span class="n">Ridge</span><span class="p">(</span><span class="n">alpha</span> <span class="o">=</span> <span class="n">alpha</span><span class="p">))</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span> 
            <span class="k">for</span> <span class="n">alpha</span> <span class="ow">in</span> <span class="n">alphas</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">cv_ridge</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">cv_ridge</span><span class="p">,</span> <span class="n">index</span> <span class="o">=</span> <span class="n">alphas</span><span class="p">)</span>
<span class="n">cv_ridge</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">title</span> <span class="o">=</span> <span class="s2">&quot;Validation - Just Do It&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;alpha&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;rmse&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[13]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0,0.5,&#39;rmse&#39;)</pre>
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
<p>注意上面的U形状曲线。 当alpha太大时，正则化太强，模型无法捕获数据中的所有复杂性。 然而，如果我们让模型过于灵活（alpha小），模型就会开始过度拟合。 根据上图，alpha = 10的值大约是正确的。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">cv_ridge</span><span class="o">.</span><span class="n">min</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[14]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0.12733734668670754</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>领回归的rmsle大概是0.127</p>
<p>让我们试试Lasso模型吧。 我们将在这里采用略微不同的方法，并使用内置的Lasso CV为我们找出最佳的alpha。 出于某种原因，Lasso CV中的alpha实际上是Ridge中的alpha。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_lasso</span> <span class="o">=</span> <span class="n">LassoCV</span><span class="p">(</span><span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mf">0.001</span><span class="p">,</span> <span class="mf">0.0005</span><span class="p">])</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">rmse_cv</span><span class="p">(</span><span class="n">model_lasso</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[16]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>0.1231442109097743</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>太好了！ lasso表现得更好，所以我们只是用这个来预测测试集。 关于lasso的另一个好处是它为你做了特色选择 - 设置它认为不重要的特征系数为零。 我们来看看系数：</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">coef</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">model_lasso</span><span class="o">.</span><span class="n">coef_</span><span class="p">,</span> <span class="n">index</span> <span class="o">=</span> <span class="n">X_train</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Lasso picked &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coef</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; variables and eliminated the other &quot;</span> <span class="o">+</span>  <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coef</span> <span class="o">==</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; variables&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Lasso picked 110 variables and eliminated the other 178 variables
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
<p>干得好Lasso。 然而，有一点需要注意的是，所选择的特征不一定是“正确的” - 特别是因为该数据集中有许多线性相关的特征（特征存在共线性）。 尝试一下在选择的样本上运行Lasso几次，看看特征选择的稳定性。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>我们可以看看最重要的特征是什么：</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">imp_coef</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">coef</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">),</span>
                     <span class="n">coef</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">tail</span><span class="p">(</span><span class="mi">10</span><span class="p">)])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">matplotlib</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;figure.figsize&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mf">8.0</span><span class="p">,</span> <span class="mf">10.0</span><span class="p">)</span>
<span class="n">imp_coef</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span> <span class="o">=</span> <span class="s2">&quot;barh&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Coefficients in the Lasso Model&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[20]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>Text(0.5,1,&#39;Coefficients in the Lasso Model&#39;)</pre>
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
<p>最重要的特征是<code>GrLivArea</code>。一些位置和房屋质量的特征也有积极的作用。 一些负面特征不太有意义，它们可能来自不平衡的分类变量。</p>
<p>另请注意，与从随机森林中获得的特征重要性不同，这些是模型中的实际系数 - 因此您可以准确地说出为什么预测价格就是这样。 这里唯一的问题是我们做了对数变换，所以实际的幅度有点难以解释。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1">#let&#39;s look at the residuals as well:</span>
<span class="n">matplotlib</span><span class="o">.</span><span class="n">rcParams</span><span class="p">[</span><span class="s1">&#39;figure.figsize&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="p">(</span><span class="mf">6.0</span><span class="p">,</span> <span class="mf">6.0</span><span class="p">)</span>

<span class="n">preds</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s2">&quot;preds&quot;</span><span class="p">:</span><span class="n">model_lasso</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_train</span><span class="p">),</span> <span class="s2">&quot;true&quot;</span><span class="p">:</span><span class="n">y</span><span class="p">})</span>
<span class="n">preds</span><span class="p">[</span><span class="s2">&quot;residuals&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">preds</span><span class="p">[</span><span class="s2">&quot;true&quot;</span><span class="p">]</span> <span class="o">-</span> <span class="n">preds</span><span class="p">[</span><span class="s2">&quot;preds&quot;</span><span class="p">]</span>
<span class="n">preds</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s2">&quot;preds&quot;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s2">&quot;residuals&quot;</span><span class="p">,</span><span class="n">kind</span> <span class="o">=</span> <span class="s2">&quot;scatter&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[21]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x23c85442d68&gt;</pre>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAxcAAALoCAYAAAAKkwhEAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAWJQAAFiUBSVIk8AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzs3X18HOV5L/zfva9aSZYVW8YYGduJDdikYCO7MbL7IHAwwRS3JKTpacBOeGnrhJ70BJpz9CSlfRKS2k/yQHqa5sWNIcE+5EkpJ5CaYoKDQWksxQQZG1pkEmNsQDbGAmRhafWyu3P+WI1YrXZm7pm5Z3dm5/f9fPJxkFazs2+z93Xf131dQtM0EBERERERuRWp9AkQEREREVF1YHBBRERERERKMLggIiIiIiIlGFwQEREREZESDC6IiIiIiEgJBhdERERERKQEgwsiIiIiIlKCwQURERERESnB4IKIiIiIiJRgcEFEREREREowuCAiIiIiIiUYXBARERERkRIMLoiIiIiISAkGF0REREREpASDCyIiIiIiUiJW6RMgY0KIVwA0ADha4VMhIiIiouq2AMCApmnvd3MQBhf+1pBKpWYsWbJkRqVPhIiIiIiqV09PD9LptOvjMLjwt6NLliyZ0d3dXenzICIiIqIqtnz5cuzfv/+o2+NwzwURERERESnB4IKIiIiIiJRgcEFEREREREowuCAiIiIiIiUYXBARERERkRIMLoiIiIiISAkGF0REREREpASDCyIiIiIiUoLBBRERERERKcHggoiIiIiIlGBwQURERERESjC4ICIiIiIiJRhcEBERERGREgwuiIiIiIhICQYXRERERESkBIMLIiIiIiJSgsEFEREREREpweCCiIiIiIiUYHBBRERERERKMLggIiIiIiIlGFwQEREREZESDC6IiIiIiEgJBhdERERERKQEgwsiIiIiIlKCwQURERERESnB4IKIiIiIiJSIVfoEiIjs6O1PY3vXUTx68ATeHhzFjLoErl06BxtbF6C5MVXp0yMiIgo1BhdEFBidh/tw6/ZnMTSanfhZb38aWzuOYEfXMWzbuAKrFjVV8AyJiIjCjWlRRBQIvf3pKYFFoaHRLG7d/ix6+9NlPjMiIiLSMbggokDY3nXUMLDQDY1msaPrWHlOiIiIiKZgcEFEgfDo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
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
<p>这个图看起来相当不错</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#28155;&#21152;xgboost:">&#28155;&#21152;xgboost:<a class="anchor-link" href="#&#28155;&#21152;xgboost:">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>让我们在线性模型中添加一个xgboost模型，看看我们是否可以提高分数：</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">xgboost</span> <span class="k">as</span> <span class="nn">xgb</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[23]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">dtrain</span> <span class="o">=</span> <span class="n">xgb</span><span class="o">.</span><span class="n">DMatrix</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="n">y</span><span class="p">)</span>
<span class="n">dtest</span> <span class="o">=</span> <span class="n">xgb</span><span class="o">.</span><span class="n">DMatrix</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="n">params</span> <span class="o">=</span> <span class="p">{</span><span class="s2">&quot;max_depth&quot;</span><span class="p">:</span><span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;eta&quot;</span><span class="p">:</span><span class="mf">0.1</span><span class="p">}</span>
<span class="n">model</span> <span class="o">=</span> <span class="n">xgb</span><span class="o">.</span><span class="n">cv</span><span class="p">(</span><span class="n">params</span><span class="p">,</span> <span class="n">dtrain</span><span class="p">,</span>  <span class="n">num_boost_round</span><span class="o">=</span><span class="mi">500</span><span class="p">,</span> <span class="n">early_stopping_rounds</span><span class="o">=</span><span class="mi">100</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 0 extra nodes, 0 pruned nodes, max_depth=0
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 2 extra nodes, 0 pruned nodes, max_depth=1
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:03] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:04] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:05] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:06] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 4 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
[15:43:07] d:\build\xgboost\xgboost-0.80.git\src\tree\updater_prune.cc:74: tree pruning end, 1 roots, 6 extra nodes, 0 pruned nodes, max_depth=2
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model</span><span class="o">.</span><span class="n">loc</span><span class="p">[</span><span class="mi">30</span><span class="p">:,[</span><span class="s2">&quot;test-rmse-mean&quot;</span><span class="p">,</span> <span class="s2">&quot;train-rmse-mean&quot;</span><span class="p">]]</span><span class="o">.</span><span class="n">plot</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[24]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x23c868e7f98&gt;</pre>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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n99vQl4XAAAAcsukSZNUXV2tJUuW6Etf+pKmT5+e3HfsscdKkn7xi19owYIF6tOnj6ZOnar+/fvrtdde04033qhHHnlEGzduVK9evSQlgvq4ceNkjNG0adN0xBFHaN++fXrvvfe0bNkyXXPNNcrLy9P8+fP10EMPaf369Zo1a5YqKysPqP77779fq1ev1je/+U1deOGFrQJqdXW1JkyYoLKyMp1zzjmqqqrSvffeq1NPPVUbN27UvHnzVFVVpalTpyoSiWjlypWaMWOGhgwZovHjxyfPM3v2bK1cuVLHHHOMzjvvPBUVFemTTz7RM888o9WrV+vrX/968tjVq1frzDPPVCQS0emnn67Pf/7z2r59u/785z/rb3/7m9auXavRo0d36XP+5S9/0apVqzR16lRdeOGFeu6557RixQpt3bpV1113nU4++WRNnDhR559/vl5//XX99a9/1fvvv6/XX3897Q69H3zwgSZNmqRt27Zp4sSJOu2001RbW6tVq1bptNNO06233qrvf//7yeO3bNmiq666Sl/96lc1ZcoUVVRU6MMPP9Rf/vIXPfroo/rrX/+q0047rVW9zd/3/Px8nX322WpoaND999+vuXPnKhAIaNasWV36/H5h3LxdqteMMZtGjx49etOmTV6XAgDIUVu2bJEkjRw5ss39lVf8zc1yumXbdVMO/LXbtumII47QrFmz0rrpkrR27VpNnjxZJ5xwgh555BH17t07uW/FihWaM2eO5s+fr5tuukmSdNlll2nx4sV66KGHdMYZZ6Sda8+ePSovL0+Gx4ULF2rRokVau3atJk2a1KWam9/bGKNHHnmkzcDY3GWfN2+eli1blnzfO++8U+edd54qKio0YcIE3XfffSosLJQkbdiwQV/96lc1ffp0Pfjgg5IS3eWKigqNHj1aL7zwgoLBYNr77N69W4ccckjyMw4dOlTBYFBPP/20Ro0alTzujTfe0Lhx4zRixAi98sorXfqcwWBQTz75pL72ta9JkuLxuE499VQ98cQTqqio0C233KJzzz03+brzzz9fy5cvb/VzmDRpkp5++mndc889+s53vpN8vrq6WpMmTdLbb7+tbdu2acCAAcnPHolE1Ldv37S6tm/frrFjx6q8vDz5e9Ty+37++efr1ltvTX6/3nzzTX3xi1/UiBEj9Oabb2b0+TvT2e9wszFjxuiV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BgxIO+a///u/tW7dOp1++uk65ZRT9Je//EVXXXWVwuGw+vTpoyuuuELTp0/XxIkT9fjjj+s3v/mNYrGYfvvb3ybPsXr1ak2ZMkW9evXStGnTNGjQIFVVVWnLli1atmyZFixYkPYZJ0+erM2bN2v06NGaO3eu4vG41qxZo5kzZ+qNN97QNddc06XP2fx9Kysr0znnnKOqqirde++9OvXUU7Vx40bNmzdPVVVVmjp1qiKRiFauXKkZM2ZoyJAhGj9+fNq5zj//fC1fvlyDBw/WmWeeqd69e+v555/X1VdfrSeffFKPP/64QqFUbL3iiisUCAQ0btw4DRo0SHv37tVTTz2lSy65RC+99JLuvPPONmv+8Y9/rDVr1iS/72vXrtUf/vAHvffee3rqqae69PldY63NmT+SNo0ePdq67Z1Hf2Ptgl7WLuhl1153tuvvDwDwjzfffNO++eab7R/Q9P8XPeJPN2zdutVKsrNmzWq1b+3atVaSlWR/97vftfn6999/38bj8VbP/+xnP7OS7L333pv+bV2wwEqya9euTXu++X3OP/98G41Gk8+/8cYbNhgM2pEjR3bpczWf73vf+56NRCKt9s+aNctKsocffrjdvn178vk9e/bYQw45xBYXF9u+ffum/W+koaHBjhw50ubn59udO3cmnz/zzDOtJPvqq6+2ep9du3a1+b7XX3992vP19fX21FNPtcYYu3nz5i5/znnz5tlYLJZ8/o477rCSbEVFhZ06daqtr69P7nv66aetJDt9+vS0c912221Wkv32t79t6+rq0vY1/9xuvvnmtOffe++9VjXFYjF73nnnWUn2+eefb/PzDxkyxH7wwQfJ5yORiJ04caKVZF944YWMPnunv8NNRo8ebSVtst3Mr4zBuCDgWA0mYBmDAQAgE8cee6zmzZvX5r6hQ4fKGNPq+fnz50uS1qxZk/H7FBcXa/HixWmd+FGjRmnChAnasmWLampqulR3fn6+brzxxrROcEtXX321Bg0alPy6d+/emjZtmurq6vSf//mfGjlyZHJfQUGBZsyYoXA4rC1btrQ6V1FRUavnnPP5u3fv1l133aXjjz9eP/7xj9OOKyws1PXXXy9rre65554ufc7i4mLdcMMNCgRScXLmzJkKhULas2ePlixZosLCwuS+iRMnqrKyUq+++mraeZYsWaJQKKTly5e3+ixX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60eXpC4sfX07YR3A/2/vvuPsuup773/WqdNnNDMa9WKr28JFso2xcQWMgyEQSkIAYxxjQuIACZCbm3opT+6T3GC41Au54cGACQFMMCGUgA02wja2sdxkSbYkq7dpmj6nr+ePtc85+0zRzEhn5pT5vl+v9dp9nzU6e0a/vfZvryUiItVIwXolaV6Rm10d6s3N7zjaTyajl0xFREREqo2C9UqyYFVutil2lNb6COBeMj3QMzzZUSIiIiJSoRSsV5KWfLBu+g7ykmXNueWnDveVokYiIiIiMosUrFeSBavz86cOcsmqBbnFxw/0jt9fRERERCqagvVK0rIyP99/hEtW5lvWHz9wqgQVEhEREZHZpGC9kkTqoL7DzWeSXNwySjjoBkfa2zlE73CihJUTERERkWJTsF5pfC+Z1gwfZrMvb/03SoURERERqSoK1iuN7yVTTh3kstWtuS1VcBUAACAASURBVMXH9itYFxEREakmCtYrja9lnb6DXH5uW27xV3u7S1AhEREREZktCtYrTUHL+gEuO6c1l7e++8QgnYOxElVMRERERIpNwXqlaT0nP9/7IvXREFtW5rtwfEit6yIiIiJVQ8F6pWlbm5/v3gPWctW69tyqbS8oWBcRERGpFgrWK03jEgjXu/lYH4z0ctW6hbnND7zQRSqdKVHlRERERKSYFKxXGmOgbU1+uWcPL1nWTEdjFIDe4QSPqlcYERERkaqgYL0S+VNhevYSCBh+a/Pi3KofPnu8BJUSERERkWJTsF6J2tfl53v2AnDTBUtzq36y44RSYURERESqgIL1SjT2JVPgklULClJh7tvVWYqaiYiIiEgRKVivRAU56/sACAQMb966PLf6rof3z3WtRERERKTIFKxXIn/Leu8+SKcAeMflqwgG3ABJv36xl13HB0pROxEREREpEgXrlaimGRq9HPV0wgXswNKWWm70vWh610MHSlA5ERERESkWBeuVatF5+fnOnbnZW69YnZu/96mj9A4n5rBSIiIiIlJMCtYrVYcvWD+ZD9a3rlrA5mVNAMRTGb752KG5rpmIiIiIFImC9Uq16Pz8vK9l3RjDrVeck1u+6+EDxJLpuayZiIiIiBSJgvVKVdCy/lzBptdeuITFTTUAdA3G+c5vDs9lzURERESkSBSsV6r29WCCbv7UAUgM5zZFQ0Fuv/rc3PL/eWAfI4nUHFdQRERERM6WgvVKFa7x9bduoXNXwebfv2wFbfURAI71x/jHH++e4wqKiIiIyNlSsF7JFm3Oz594pmBTXSTEX75mU275q48c5IHnNaqpiIiISCVRsF7JllyYnz/21LjNb9qyjOs3duSW//RbT3G4d2QuaiYiIiIiRaBgvZItvSg/f/zpcZuNMfyvN1/AoqYoAH0jSf74G9vVO4yIiIhIhVCwXsn8LeudOyE1fgCk9oYoX3j7FkIBA8CzR/v56A92jttPRERERMqPgvVKVrsAWla5+XQCunZNuNvWVa38zU35/PVvPnZI3TmKiIiIVAAF65XOnwozQd561i1XrOa3L1yaW/6be3fw3LH+2ayZiIiIiJwlBeuVzp8Kc/SJSXczxvD/vvElrOtoACCeyvDeu5+gb2R86oyIiIiIlAcF65Vu+WX5+cOPnnbX+miIL968lYZoyO3eO8pb//nXdA7GZrOGIiIiInKGFKxXumVbIRB28127YaT3tLuvWdjAJ95yQW5594lBfveLj3DklLp0FBERESk3CtYrXaSuMG/90K+nPOTGzUu48y0XEvR6iDnQM8JNn/kVX/7VfjIZO1s1FREREZEZUrBeDVZenp8/9Mi0DnnT1uV84e1biATdJdA/muTj/7mT27/2G3qG4rNRSxERERGZIQXr1WDlFfn5gw9P+7BXn7+Yr912GStb63Lr7t/dyVX/6xd86mcvaPAkERERkRJTsF4NVl4OuJQWjj0Jo33TPvTyc9u474PX8IdXn5tbN5JI8+n79/Caz2zjcK9y2UVERERKRcF6Nahrzeet2zQc2DajwyOhAH/5mk38f++6hI2LG3PrX+wa5ve+9Ajb9nRhrXLZRUREROaagvVqseb6/Py+n5/RKa7fuIgfvv8qPv6GzURC7tI41h/j5i8/xu984WG+/fhh9ncPF6O2IiIiIjINoVJXQIpkzfWw7U43f4bBOkAwYLj58lWsbqvjPV97glEvb/2pw308ddil11yzfiG/f9lKrt2wkJpw8KyrLiIiIiITU8t6tVh+GYTr3fypA9C996xOd9W6hdz3oWu4+fJVuR5jsh58oYv33v0El/79ffz1957lWN/oWX2WiIiIiExMwXq1CEXg3Gvzy8//8KxPuayllo+/YTPb/uI6/vzVG7h2w0KMyW8fjKX4xqOHuPYTD/Durz7OT587odx2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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_xgb</span> <span class="o">=</span> <span class="n">xgb</span><span class="o">.</span><span class="n">XGBRegressor</span><span class="p">(</span><span class="n">n_estimators</span><span class="o">=</span><span class="mi">360</span><span class="p">,</span> <span class="n">max_depth</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">learning_rate</span><span class="o">=</span><span class="mf">0.1</span><span class="p">)</span> <span class="c1">#the params were tuned using xgb.cv</span>
<span class="n">model_xgb</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[25]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>XGBRegressor(base_score=0.5, booster=&#39;gbtree&#39;, colsample_bylevel=1,
       colsample_bytree=1, gamma=0, learning_rate=0.1, max_delta_step=0,
       max_depth=2, min_child_weight=1, missing=None, n_estimators=360,
       n_jobs=1, nthread=None, objective=&#39;reg:linear&#39;, random_state=0,
       reg_alpha=0, reg_lambda=1, scale_pos_weight=1, seed=None,
       silent=True, subsample=1)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">xgb_preds</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">expm1</span><span class="p">(</span><span class="n">model_xgb</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">))</span>
<span class="n">lasso_preds</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">expm1</span><span class="p">(</span><span class="n">model_lasso</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">predictions</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s2">&quot;xgb&quot;</span><span class="p">:</span><span class="n">xgb_preds</span><span class="p">,</span> <span class="s2">&quot;lasso&quot;</span><span class="p">:</span><span class="n">lasso_preds</span><span class="p">})</span>
<span class="n">predictions</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s2">&quot;xgb&quot;</span><span class="p">,</span> <span class="n">y</span> <span class="o">=</span> <span class="s2">&quot;lasso&quot;</span><span class="p">,</span> <span class="n">kind</span> <span class="o">=</span> <span class="s2">&quot;scatter&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[27]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x23c86896dd8&gt;</pre>
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
<p>很多时候，对不相关的结果进行加权平均是有意义的 - 这通常可以提高分数，尽管在这种情况下它没有那么大帮助。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">preds</span> <span class="o">=</span> <span class="mf">0.7</span><span class="o">*</span><span class="n">lasso_preds</span> <span class="o">+</span> <span class="mf">0.3</span><span class="o">*</span><span class="n">xgb_preds</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">solution</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">({</span><span class="s2">&quot;id&quot;</span><span class="p">:</span><span class="n">test</span><span class="o">.</span><span class="n">Id</span><span class="p">,</span> <span class="s2">&quot;SalePrice&quot;</span><span class="p">:</span><span class="n">preds</span><span class="p">})</span>
<span class="n">solution</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s2">&quot;ridge_sol.csv&quot;</span><span class="p">,</span> <span class="n">index</span> <span class="o">=</span> <span class="kc">False</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Trying-out-keras?">Trying out keras?<a class="anchor-link" href="#Trying-out-keras?">&#182;</a></h3><p>前馈神经网络似乎效果并不好......我也不知道为什么。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">from</span> <span class="nn">keras.layers</span> <span class="k">import</span> <span class="n">Dense</span>
<span class="kn">from</span> <span class="nn">keras.models</span> <span class="k">import</span> <span class="n">Sequential</span>
<span class="kn">from</span> <span class="nn">keras.regularizers</span> <span class="k">import</span> <span class="n">l1</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="k">import</span> <span class="n">StandardScaler</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">train_test_split</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stderr output_text">
<pre>C:\Python\Anaconda3\lib\site-packages\h5py\__init__.py:36: FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
  from ._conv import register_converters as _register_converters
Using TensorFlow backend.
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_train</span> <span class="o">=</span> <span class="n">StandardScaler</span><span class="p">()</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">X_train</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[32]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_tr</span><span class="p">,</span> <span class="n">X_val</span><span class="p">,</span> <span class="n">y_tr</span><span class="p">,</span> <span class="n">y_val</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="mi">3</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[33]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_tr</span><span class="o">.</span><span class="n">shape</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[33]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>(1095, 288)</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[34]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">X_tr</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[34]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>array([[ 1.00573733,  0.68066137, -0.46001991, ..., -0.11785113,
         0.4676514 , -0.30599503],
       [-1.12520184,  0.60296111,  0.03113183, ..., -0.11785113,
         0.4676514 , -0.30599503],
       [-1.12520184, -0.02865265, -0.74027492, ..., -0.11785113,
         0.4676514 , -0.30599503],
       ...,
       [ 0.16426234, -0.87075036, -0.81954431, ..., -0.11785113,
        -2.13834494, -0.30599503],
       [ 0.92361154, -0.30038284, -0.44275864, ..., -0.11785113,
         0.4676514 , -0.30599503],
       [ 0.83656519,  1.98505948,  0.46455838, ..., -0.11785113,
         0.4676514 , -0.30599503]])</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model</span> <span class="o">=</span> <span class="n">Sequential</span><span class="p">()</span>
<span class="c1">#model.add(Dense(256, activation=&quot;relu&quot;, input_dim = X_train.shape[1]))</span>
<span class="n">model</span><span class="o">.</span><span class="n">add</span><span class="p">(</span><span class="n">Dense</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">input_dim</span> <span class="o">=</span> <span class="n">X_train</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">],</span> <span class="n">W_regularizer</span><span class="o">=</span><span class="n">l1</span><span class="p">(</span><span class="mf">0.001</span><span class="p">)))</span>

<span class="n">model</span><span class="o">.</span><span class="n">compile</span><span class="p">(</span><span class="n">loss</span> <span class="o">=</span> <span class="s2">&quot;mse&quot;</span><span class="p">,</span> <span class="n">optimizer</span> <span class="o">=</span> <span class="s2">&quot;adam&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stderr output_text">
<pre>C:\Python\Anaconda3\lib\site-packages\ipykernel_launcher.py:3: UserWarning: Update your `Dense` call to the Keras 2 API: `Dense(1, input_dim=288, kernel_regularizer=&lt;keras.reg...)`
  This is separate from the ipykernel package so we can avoid doing imports until
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model</span><span class="o">.</span><span class="n">summary</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
dense_1 (Dense)              (None, 1)                 289       
=================================================================
Total params: 289
Trainable params: 289
Non-trainable params: 0
_________________________________________________________________
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[37]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">hist</span> <span class="o">=</span> <span class="n">model</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_tr</span><span class="p">,</span> <span class="n">y_tr</span><span class="p">,</span> <span class="n">validation_data</span> <span class="o">=</span> <span class="p">(</span><span class="n">X_val</span><span class="p">,</span> <span class="n">y_val</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Train on 1095 samples, validate on 365 samples
Epoch 1/1
1095/1095 [==============================] - 0s 185us/step - loss: 147.0254 - val_loss: 149.9535
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">model</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_val</span><span class="p">)[:,</span><span class="mi">0</span><span class="p">])</span><span class="o">.</span><span class="n">hist</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt output_prompt">Out[38]:</div>




<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.axes._subplots.AxesSubplot at 0x23c8de79ba8&gt;</pre>
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
    </div>
  </div>
</body>

 


</html>
