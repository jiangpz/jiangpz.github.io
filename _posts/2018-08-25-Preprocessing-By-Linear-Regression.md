---
layout: post
title:  "Preprocessing By Linear Regression"
excerpt: "Kaggle House Prices 使用线性回归预测房价"
date:   2018-08-25 08:01:08 +0800
categories: Kaggle
tags: [Kaggle, Modeling]
comments: true
---
<html>
<head><meta charset="utf-8" />
<title>Preprocessing By Linear Regression</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
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
<p>原文地址：<a href="https://www.kaggle.com/juliencs/a-study-on-regression-applied-to-the-ames-dataset">https://www.kaggle.com/juliencs/a-study-on-regression-applied-to-the-ames-dataset</a></p>
<h3 id="&#20171;&#32461;">&#20171;&#32461;<a class="anchor-link" href="#&#20171;&#32461;">&#182;</a></h3><p>这个Kernel试图利用每一个技巧来释放线性回归的全部功能，包括大量的预处理和几个正则化算法。在看这个贴子之前最好了解过数据集和数据预处理的一些知识。</p>
<p>在撰写本文时，它在公共LB上获得了大约0.121的分数，仅使用回归，没有RF，没有xgboost，没有集成学习等。所有评论/更正都非常受欢迎。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Imports</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">from</span> <span class="nn">sklearn.model_selection</span> <span class="k">import</span> <span class="n">cross_val_score</span><span class="p">,</span> <span class="n">train_test_split</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="k">import</span> <span class="n">StandardScaler</span>
<span class="kn">from</span> <span class="nn">sklearn.linear_model</span> <span class="k">import</span> <span class="n">LinearRegression</span><span class="p">,</span> <span class="n">RidgeCV</span><span class="p">,</span> <span class="n">LassoCV</span><span class="p">,</span> <span class="n">ElasticNetCV</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="k">import</span> <span class="n">mean_squared_error</span><span class="p">,</span> <span class="n">make_scorer</span>
<span class="kn">from</span> <span class="nn">scipy.stats</span> <span class="k">import</span> <span class="n">skew</span>
<span class="kn">from</span> <span class="nn">IPython.display</span> <span class="k">import</span> <span class="n">display</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>

<span class="c1"># Definitions</span>
<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.float_format&#39;</span><span class="p">,</span> <span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s1">&#39;</span><span class="si">%.3f</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">x</span><span class="p">)</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
<span class="c1">#njobs = 4</span>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Get data</span>
<span class="n">train</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s2">&quot;input/train.csv&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;train : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>train : (1460, 81)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Check for duplicates</span>
<span class="n">idsUnique</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="nb">set</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">Id</span><span class="p">))</span>
<span class="n">idsTotal</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">]</span>
<span class="n">idsDupli</span> <span class="o">=</span> <span class="n">idsTotal</span> <span class="o">-</span> <span class="n">idsUnique</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;There are &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">idsDupli</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot; duplicate IDs for &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">idsTotal</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot; total entries&quot;</span><span class="p">)</span>

<span class="c1"># Drop Id column</span>
<span class="n">train</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s2">&quot;Id&quot;</span><span class="p">,</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">,</span> <span class="n">inplace</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>There are 0 duplicate IDs for 1460 total entries
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
<p><strong>数据预处理</strong></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Looking for outliers, as indicated in https://ww2.amstat.org/publications/jse/v19n3/decock.pdf</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">GrLivArea</span><span class="p">,</span> <span class="n">train</span><span class="o">.</span><span class="n">SalePrice</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Looking for outliers&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;GrLivArea&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="n">train</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="n">train</span><span class="o">.</span><span class="n">GrLivArea</span> <span class="o">&lt;</span> <span class="mi">4000</span><span class="p">]</span>
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
<p>右下角似乎有2个极端异常值，真正的大房子以非常便宜的价格出售。 更一般地说，数据集的作者建议从数据集中删除“任何超过4000平方英尺的房屋”。  <a href="https://ww2.amstat.org/publications/jse/v19n3/decock.pdf">https://ww2.amstat.org/publications/jse/v19n3/decock.pdf</a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Log transform the target for official scoring</span>
<span class="n">train</span><span class="o">.</span><span class="n">SalePrice</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">log1p</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">SalePrice</span><span class="p">)</span>
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
<p>做对数变换，昂贵的房屋和廉价房屋的预测错误将同样影响结果。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Handle missing values for features where median/mean or most common value doesn&#39;t make sense</span>

<span class="c1"># Alley : data description says NA means &quot;no alley access&quot;</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Alley&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Alley&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
<span class="c1"># BedroomAbvGr : NA most likely means 0</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BedroomAbvGr&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BedroomAbvGr&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># BsmtQual etc : data description says NA for basement features is &quot;no basement&quot;</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtQual&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtCond&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtCond&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtExposure&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtExposure&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtFinType1&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtFinType1&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtFinType2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtFinType2&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtFullBath&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtFullBath&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtHalfBath&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtHalfBath&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtUnfSF&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;BsmtUnfSF&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># CentralAir : NA most likely means No</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;CentralAir&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;CentralAir&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;N&quot;</span><span class="p">)</span>
<span class="c1"># Condition : NA most likely means Normal</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Condition1&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Condition1&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;Norm&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Condition2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Condition2&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;Norm&quot;</span><span class="p">)</span>
<span class="c1"># EnclosedPorch : NA most likely means no enclosed porch</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;EnclosedPorch&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;EnclosedPorch&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># External stuff : NA most likely means average</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;ExterCond&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;ExterCond&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;TA&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;ExterQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;ExterQual&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;TA&quot;</span><span class="p">)</span>
<span class="c1"># Fence : data description says NA means &quot;no fence&quot;</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Fence&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Fence&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="c1"># FireplaceQu : data description says NA means &quot;no fireplace&quot;</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;FireplaceQu&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;FireplaceQu&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Fireplaces&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Fireplaces&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># Functional : data description says NA means typical</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Functional&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Functional&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;Typ&quot;</span><span class="p">)</span>
<span class="c1"># GarageType etc : data description says NA for garage features is &quot;no garage&quot;</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageType&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageType&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageFinish&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageFinish&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageQual&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageCond&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageCond&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageArea&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageArea&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageCars&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;GarageCars&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># HalfBath : NA most likely means no half baths above grade</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;HalfBath&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;HalfBath&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># HeatingQC : NA most likely means typical</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;HeatingQC&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;HeatingQC&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;TA&quot;</span><span class="p">)</span>
<span class="c1"># KitchenAbvGr : NA most likely means 0</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;KitchenAbvGr&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;KitchenAbvGr&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># KitchenQual : NA most likely means typical</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;KitchenQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;KitchenQual&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;TA&quot;</span><span class="p">)</span>
<span class="c1"># LotFrontage : NA most likely means no lot frontage</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;LotFrontage&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;LotFrontage&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># LotShape : NA most likely means regular</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;LotShape&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;LotShape&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;Reg&quot;</span><span class="p">)</span>
<span class="c1"># MasVnrType : NA most likely means no veneer</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MasVnrType&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MasVnrType&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;None&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MasVnrArea&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MasVnrArea&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># MiscFeature : data description says NA means &quot;no misc feature&quot;</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MiscFeature&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MiscFeature&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MiscVal&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;MiscVal&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># OpenPorchSF : NA most likely means no open porch</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;OpenPorchSF&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;OpenPorchSF&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># PavedDrive : NA most likely means not paved</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;PavedDrive&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;PavedDrive&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;N&quot;</span><span class="p">)</span>
<span class="c1"># PoolQC : data description says NA means &quot;no pool&quot;</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;PoolQC&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;PoolQC&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;No&quot;</span><span class="p">)</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;PoolArea&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;PoolArea&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># SaleCondition : NA most likely means normal sale</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;SaleCondition&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;SaleCondition&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;Normal&quot;</span><span class="p">)</span>
<span class="c1"># ScreenPorch : NA most likely means no screen porch</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;ScreenPorch&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;ScreenPorch&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># TotRmsAbvGrd : NA most likely means 0</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;TotRmsAbvGrd&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;TotRmsAbvGrd&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
<span class="c1"># Utilities : NA most likely means all public utilities</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Utilities&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;Utilities&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="s2">&quot;AllPub&quot;</span><span class="p">)</span>
<span class="c1"># WoodDeckSF : NA most likely means no wood deck</span>
<span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;WoodDeckSF&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="s2">&quot;WoodDeckSF&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Some numerical features are actually really categories</span>
<span class="n">train</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="s2">&quot;MSSubClass&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="mi">20</span> <span class="p">:</span> <span class="s2">&quot;SC20&quot;</span><span class="p">,</span> <span class="mi">30</span> <span class="p">:</span> <span class="s2">&quot;SC30&quot;</span><span class="p">,</span> <span class="mi">40</span> <span class="p">:</span> <span class="s2">&quot;SC40&quot;</span><span class="p">,</span> <span class="mi">45</span> <span class="p">:</span> <span class="s2">&quot;SC45&quot;</span><span class="p">,</span> 
                                       <span class="mi">50</span> <span class="p">:</span> <span class="s2">&quot;SC50&quot;</span><span class="p">,</span> <span class="mi">60</span> <span class="p">:</span> <span class="s2">&quot;SC60&quot;</span><span class="p">,</span> <span class="mi">70</span> <span class="p">:</span> <span class="s2">&quot;SC70&quot;</span><span class="p">,</span> <span class="mi">75</span> <span class="p">:</span> <span class="s2">&quot;SC75&quot;</span><span class="p">,</span> 
                                       <span class="mi">80</span> <span class="p">:</span> <span class="s2">&quot;SC80&quot;</span><span class="p">,</span> <span class="mi">85</span> <span class="p">:</span> <span class="s2">&quot;SC85&quot;</span><span class="p">,</span> <span class="mi">90</span> <span class="p">:</span> <span class="s2">&quot;SC90&quot;</span><span class="p">,</span> <span class="mi">120</span> <span class="p">:</span> <span class="s2">&quot;SC120&quot;</span><span class="p">,</span> 
                                       <span class="mi">150</span> <span class="p">:</span> <span class="s2">&quot;SC150&quot;</span><span class="p">,</span> <span class="mi">160</span> <span class="p">:</span> <span class="s2">&quot;SC160&quot;</span><span class="p">,</span> <span class="mi">180</span> <span class="p">:</span> <span class="s2">&quot;SC180&quot;</span><span class="p">,</span> <span class="mi">190</span> <span class="p">:</span> <span class="s2">&quot;SC190&quot;</span><span class="p">},</span>
                       <span class="s2">&quot;MoSold&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="mi">1</span> <span class="p">:</span> <span class="s2">&quot;Jan&quot;</span><span class="p">,</span> <span class="mi">2</span> <span class="p">:</span> <span class="s2">&quot;Feb&quot;</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="s2">&quot;Mar&quot;</span><span class="p">,</span> <span class="mi">4</span> <span class="p">:</span> <span class="s2">&quot;Apr&quot;</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="s2">&quot;May&quot;</span><span class="p">,</span> <span class="mi">6</span> <span class="p">:</span> <span class="s2">&quot;Jun&quot;</span><span class="p">,</span>
                                   <span class="mi">7</span> <span class="p">:</span> <span class="s2">&quot;Jul&quot;</span><span class="p">,</span> <span class="mi">8</span> <span class="p">:</span> <span class="s2">&quot;Aug&quot;</span><span class="p">,</span> <span class="mi">9</span> <span class="p">:</span> <span class="s2">&quot;Sep&quot;</span><span class="p">,</span> <span class="mi">10</span> <span class="p">:</span> <span class="s2">&quot;Oct&quot;</span><span class="p">,</span> <span class="mi">11</span> <span class="p">:</span> <span class="s2">&quot;Nov&quot;</span><span class="p">,</span> <span class="mi">12</span> <span class="p">:</span> <span class="s2">&quot;Dec&quot;</span><span class="p">}</span>
                      <span class="p">})</span>
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
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Encode some categorical features as ordered numbers when there is information in the order</span>
<span class="n">train</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="s2">&quot;Alley&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Grvl&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Pave&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">},</span>
                       <span class="s2">&quot;BsmtCond&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;BsmtExposure&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Mn&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Av&quot;</span><span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">},</span>
                       <span class="s2">&quot;BsmtFinType1&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Unf&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;LwQ&quot;</span><span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;Rec&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;BLQ&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> 
                                         <span class="s2">&quot;ALQ&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">,</span> <span class="s2">&quot;GLQ&quot;</span> <span class="p">:</span> <span class="mi">6</span><span class="p">},</span>
                       <span class="s2">&quot;BsmtFinType2&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Unf&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;LwQ&quot;</span><span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;Rec&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;BLQ&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> 
                                         <span class="s2">&quot;ALQ&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">,</span> <span class="s2">&quot;GLQ&quot;</span> <span class="p">:</span> <span class="mi">6</span><span class="p">},</span>
                       <span class="s2">&quot;BsmtQual&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span><span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;ExterCond&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span><span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span><span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;ExterQual&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span><span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span><span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;FireplaceQu&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;Functional&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Sal&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Sev&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;Maj2&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Maj1&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Mod&quot;</span><span class="p">:</span> <span class="mi">5</span><span class="p">,</span> 
                                       <span class="s2">&quot;Min2&quot;</span> <span class="p">:</span> <span class="mi">6</span><span class="p">,</span> <span class="s2">&quot;Min1&quot;</span> <span class="p">:</span> <span class="mi">7</span><span class="p">,</span> <span class="s2">&quot;Typ&quot;</span> <span class="p">:</span> <span class="mi">8</span><span class="p">},</span>
                       <span class="s2">&quot;GarageCond&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;GarageQual&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;HeatingQC&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;KitchenQual&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Po&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">5</span><span class="p">},</span>
                       <span class="s2">&quot;LandSlope&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Sev&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Mod&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;Gtl&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">},</span>
                       <span class="s2">&quot;LotShape&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;IR3&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;IR2&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;IR1&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Reg&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">},</span>
                       <span class="s2">&quot;PavedDrive&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;N&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;P&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Y&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">},</span>
                       <span class="s2">&quot;PoolQC&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;No&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Fa&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;TA&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;Gd&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;Ex&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">},</span>
                       <span class="s2">&quot;Street&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;Grvl&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;Pave&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">},</span>
                       <span class="s2">&quot;Utilities&quot;</span> <span class="p">:</span> <span class="p">{</span><span class="s2">&quot;ELO&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;NoSeWa&quot;</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="s2">&quot;NoSewr&quot;</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="s2">&quot;AllPub&quot;</span> <span class="p">:</span> <span class="mi">4</span><span class="p">}}</span>
                     <span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>接着我们通过下面三种方式创建新特征 :</p>
<ol>
<li>简化现有特征</li>
<li>将现有特征做组合</li>
<li>将最重要的10个特征做成多项式</li>
</ol>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Create new features</span>
<span class="c1"># 1* Simplifications of existing features</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">OverallQual</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                       <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">6</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="c1"># average</span>
                                                       <span class="mi">7</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">8</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">9</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">10</span> <span class="p">:</span> <span class="mi">3</span> <span class="c1"># good</span>
                                                      <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallCond&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">OverallCond</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                       <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">6</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="c1"># average</span>
                                                       <span class="mi">7</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">8</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">9</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">10</span> <span class="p">:</span> <span class="mi">3</span> <span class="c1"># good</span>
                                                      <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplPoolQC&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">PoolQC</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                             <span class="mi">3</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                            <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplGarageCond&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">GarageCond</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                     <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                     <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                    <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplGarageQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">GarageQual</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                     <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                     <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                    <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplFireplaceQu&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">FireplaceQu</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                       <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                       <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                      <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplFireplaceQu&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">FireplaceQu</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                       <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                       <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                      <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplFunctional&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">Functional</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                     <span class="mi">3</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="c1"># major</span>
                                                     <span class="mi">5</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">6</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">7</span> <span class="p">:</span> <span class="mi">3</span><span class="p">,</span> <span class="c1"># minor</span>
                                                     <span class="mi">8</span> <span class="p">:</span> <span class="mi">4</span> <span class="c1"># typical</span>
                                                    <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplKitchenQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">KitchenQual</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                       <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                       <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                      <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplHeatingQC&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">HeatingQC</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                   <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                   <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                  <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplBsmtFinType1&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">BsmtFinType1</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># unfinished</span>
                                                         <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># rec room</span>
                                                         <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">6</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># living quarters</span>
                                                        <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplBsmtFinType2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">BsmtFinType2</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># unfinished</span>
                                                         <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># rec room</span>
                                                         <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">6</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># living quarters</span>
                                                        <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplBsmtCond&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">BsmtCond</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                 <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                 <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplBsmtQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">BsmtQual</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                 <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                 <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplExterCond&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">ExterCond</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                   <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                   <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                  <span class="p">})</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplExterQual&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">ExterQual</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="mi">1</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># bad</span>
                                                   <span class="mi">2</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="c1"># average</span>
                                                   <span class="mi">4</span> <span class="p">:</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">5</span> <span class="p">:</span> <span class="mi">2</span> <span class="c1"># good</span>
                                                  <span class="p">})</span>

<span class="c1"># 2* Combinations of existing features</span>
<span class="c1"># Overall quality of the house</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallGrade&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallQual&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallCond&quot;</span><span class="p">]</span>
<span class="c1"># Overall quality of the garage</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageGrade&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageQual&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageCond&quot;</span><span class="p">]</span>
<span class="c1"># Overall quality of the exterior</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterGrade&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterQual&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterCond&quot;</span><span class="p">]</span>
<span class="c1"># Overall kitchen score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenAbvGr&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenQual&quot;</span><span class="p">]</span>
<span class="c1"># Overall fireplace score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;FireplaceScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;Fireplaces&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;FireplaceQu&quot;</span><span class="p">]</span>
<span class="c1"># Overall garage score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageArea&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageQual&quot;</span><span class="p">]</span>
<span class="c1"># Overall pool score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;PoolScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;PoolArea&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;PoolQC&quot;</span><span class="p">]</span>
<span class="c1"># Simplified overall quality of the house</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallGrade&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallCond&quot;</span><span class="p">]</span>
<span class="c1"># Simplified overall quality of the exterior</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplExterGrade&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplExterQual&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplExterCond&quot;</span><span class="p">]</span>
<span class="c1"># Simplified overall pool score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplPoolScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;PoolArea&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplPoolQC&quot;</span><span class="p">]</span>
<span class="c1"># Simplified overall garage score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplGarageScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageArea&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplGarageQual&quot;</span><span class="p">]</span>
<span class="c1"># Simplified overall fireplace score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplFireplaceScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;Fireplaces&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplFireplaceQu&quot;</span><span class="p">]</span>
<span class="c1"># Simplified overall kitchen score</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplKitchenScore&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenAbvGr&quot;</span><span class="p">]</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplKitchenQual&quot;</span><span class="p">]</span>
<span class="c1"># Total number of bathrooms</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBath&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;BsmtFullBath&quot;</span><span class="p">]</span> <span class="o">+</span> <span class="p">(</span><span class="mf">0.5</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;BsmtHalfBath&quot;</span><span class="p">])</span> <span class="o">+</span> \
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;FullBath&quot;</span><span class="p">]</span> <span class="o">+</span> <span class="p">(</span><span class="mf">0.5</span> <span class="o">*</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;HalfBath&quot;</span><span class="p">])</span>
<span class="c1"># Total SF for house (incl. basement)</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllSF&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GrLivArea&quot;</span><span class="p">]</span> <span class="o">+</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBsmtSF&quot;</span><span class="p">]</span>
<span class="c1"># Total SF for 1st + 2nd floors</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllFlrsSF&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;1stFlrSF&quot;</span><span class="p">]</span> <span class="o">+</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;2ndFlrSF&quot;</span><span class="p">]</span>
<span class="c1"># Total SF for porch</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllPorchSF&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;OpenPorchSF&quot;</span><span class="p">]</span> <span class="o">+</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;EnclosedPorch&quot;</span><span class="p">]</span> <span class="o">+</span> \
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;3SsnPorch&quot;</span><span class="p">]</span> <span class="o">+</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;ScreenPorch&quot;</span><span class="p">]</span>
<span class="c1"># Has masonry veneer or not</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;HasMasVnr&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">MasVnrType</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="s2">&quot;BrkCmn&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;BrkFace&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;CBlock&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> 
                                               <span class="s2">&quot;Stone&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">,</span> <span class="s2">&quot;None&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">})</span>
<span class="c1"># House completed before sale or not</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;BoughtOffPlan&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">SaleCondition</span><span class="o">.</span><span class="n">replace</span><span class="p">({</span><span class="s2">&quot;Abnorml&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Alloca&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;AdjLand&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> 
                                                      <span class="s2">&quot;Family&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Normal&quot;</span> <span class="p">:</span> <span class="mi">0</span><span class="p">,</span> <span class="s2">&quot;Partial&quot;</span> <span class="p">:</span> <span class="mi">1</span><span class="p">})</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Find most important features relative to target</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Find most important features relative to target&quot;</span><span class="p">)</span>
<span class="n">corr</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">corr</span><span class="p">()</span>
<span class="n">corr</span><span class="o">.</span><span class="n">sort_values</span><span class="p">([</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">],</span> <span class="n">ascending</span> <span class="o">=</span> <span class="kc">False</span><span class="p">,</span> <span class="n">inplace</span> <span class="o">=</span> <span class="kc">True</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">corr</span><span class="o">.</span><span class="n">SalePrice</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Find most important features relative to target
SalePrice            1.000
OverallQual          0.819
AllSF                0.817
AllFlrsSF            0.729
GrLivArea            0.719
SimplOverallQual     0.708
ExterQual            0.681
GarageCars           0.680
TotalBath            0.673
KitchenQual          0.667
GarageScore          0.657
GarageArea           0.655
TotalBsmtSF          0.642
SimplExterQual       0.636
SimplGarageScore     0.631
BsmtQual             0.615
1stFlrSF             0.614
SimplKitchenQual     0.610
OverallGrade         0.604
SimplBsmtQual        0.594
FullBath             0.591
YearBuilt            0.589
ExterGrade           0.587
YearRemodAdd         0.569
FireplaceQu          0.547
GarageYrBlt          0.544
TotRmsAbvGrd         0.533
SimplOverallGrade    0.527
SimplKitchenScore    0.523
FireplaceScore       0.518
                     ...  
SimplBsmtCond        0.204
BedroomAbvGr         0.204
AllPorchSF           0.199
LotFrontage          0.174
SimplFunctional      0.137
Functional           0.136
ScreenPorch          0.124
SimplBsmtFinType2    0.105
Street               0.058
3SsnPorch            0.056
ExterCond            0.051
PoolArea             0.041
SimplPoolScore       0.040
SimplPoolQC          0.040
PoolScore            0.040
PoolQC               0.038
BsmtFinType2         0.016
Utilities            0.013
BsmtFinSF2           0.006
BsmtHalfBath        -0.015
MiscVal             -0.020
SimplOverallCond    -0.028
YrSold              -0.034
OverallCond         -0.037
LowQualFinSF        -0.038
LandSlope           -0.040
SimplExterCond      -0.042
KitchenAbvGr        -0.148
EnclosedPorch       -0.149
LotShape            -0.286
Name: SalePrice, Length: 88, dtype: float64
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Create new features</span>
<span class="c1"># 3* Polynomials on the top 10 existing features</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallQual-s2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallQual-s3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallQual-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;OverallQual&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllSF-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllSF&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllSF-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllSF&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllSF-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllSF&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllFlrsSF-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllFlrsSF&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllFlrsSF-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllFlrsSF&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllFlrsSF-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;AllFlrsSF&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GrLivArea-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GrLivArea&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GrLivArea-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GrLivArea&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GrLivArea-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;GrLivArea&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual-s2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual-s3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;SimplOverallQual&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterQual-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterQual-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterQual-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;ExterQual&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageCars-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageCars&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageCars-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageCars&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageCars-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageCars&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBath-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBath&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBath-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBath&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBath-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;TotalBath&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenQual-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenQual-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenQual&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenQual-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;KitchenQual&quot;</span><span class="p">])</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageScore-2&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageScore&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">2</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageScore-3&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageScore&quot;</span><span class="p">]</span> <span class="o">**</span> <span class="mi">3</span>
<span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageScore-Sq&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="n">train</span><span class="p">[</span><span class="s2">&quot;GarageScore&quot;</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Differentiate numerical features (minus the target) and categorical features</span>
<span class="n">categorical_features</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">select_dtypes</span><span class="p">(</span><span class="n">include</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;object&quot;</span><span class="p">])</span><span class="o">.</span><span class="n">columns</span>
<span class="n">numerical_features</span> <span class="o">=</span> <span class="n">train</span><span class="o">.</span><span class="n">select_dtypes</span><span class="p">(</span><span class="n">exclude</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;object&quot;</span><span class="p">])</span><span class="o">.</span><span class="n">columns</span>
<span class="n">numerical_features</span> <span class="o">=</span> <span class="n">numerical_features</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="s2">&quot;SalePrice&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Numerical features : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">numerical_features</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Categorical features : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">categorical_features</span><span class="p">)))</span>
<span class="n">train_num</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="n">numerical_features</span><span class="p">]</span>
<span class="n">train_cat</span> <span class="o">=</span> <span class="n">train</span><span class="p">[</span><span class="n">categorical_features</span><span class="p">]</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Numerical features : 117
Categorical features : 26
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Handle remaining missing values for numerical features by using median as replacement</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;NAs for numerical features in train : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train_num</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">sum</span><span class="p">()))</span>
<span class="n">train_num</span> <span class="o">=</span> <span class="n">train_num</span><span class="o">.</span><span class="n">fillna</span><span class="p">(</span><span class="n">train_num</span><span class="o">.</span><span class="n">median</span><span class="p">())</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Remaining NAs for numerical features in train : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train_num</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">sum</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>NAs for numerical features in train : 81
Remaining NAs for numerical features in train : 0
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Log transform of the skewed numerical features to lessen impact of outliers</span>
<span class="c1"># Inspired by Alexandru Papiu&#39;s script : https://www.kaggle.com/apapiu/house-prices-advanced-regression-techniques/regularized-linear-models</span>
<span class="c1"># As a general rule of thumb, a skewness with an absolute value &gt; 0.5 is considered at least moderately skewed</span>
<span class="n">skewness</span> <span class="o">=</span> <span class="n">train_num</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">skew</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>
<span class="n">skewness</span> <span class="o">=</span> <span class="n">skewness</span><span class="p">[</span><span class="nb">abs</span><span class="p">(</span><span class="n">skewness</span><span class="p">)</span> <span class="o">&gt;</span> <span class="mf">0.5</span><span class="p">]</span>
<span class="nb">print</span><span class="p">(</span><span class="nb">str</span><span class="p">(</span><span class="n">skewness</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">0</span><span class="p">])</span> <span class="o">+</span> <span class="s2">&quot; skewed numerical features to log transform&quot;</span><span class="p">)</span>
<span class="n">skewed_features</span> <span class="o">=</span> <span class="n">skewness</span><span class="o">.</span><span class="n">index</span>
<span class="n">train_num</span><span class="p">[</span><span class="n">skewed_features</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">log1p</span><span class="p">(</span><span class="n">train_num</span><span class="p">[</span><span class="n">skewed_features</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>86 skewed numerical features to log transform
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Create dummy features for categorical values via one-hot encoding</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;NAs for categorical features in train : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train_cat</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">sum</span><span class="p">()))</span>
<span class="n">train_cat</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">get_dummies</span><span class="p">(</span><span class="n">train_cat</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Remaining NAs for categorical features in train : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train_cat</span><span class="o">.</span><span class="n">isnull</span><span class="p">()</span><span class="o">.</span><span class="n">values</span><span class="o">.</span><span class="n">sum</span><span class="p">()))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>NAs for categorical features in train : 1
Remaining NAs for categorical features in train : 0
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
<h3 id="&#35757;&#32451;&#27169;&#22411;">&#35757;&#32451;&#27169;&#22411;<a class="anchor-link" href="#&#35757;&#32451;&#27169;&#22411;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Join categorical and numerical features</span>
<span class="n">train</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">train_num</span><span class="p">,</span> <span class="n">train_cat</span><span class="p">],</span> <span class="n">axis</span> <span class="o">=</span> <span class="mi">1</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;New number of features : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">train</span><span class="o">.</span><span class="n">shape</span><span class="p">[</span><span class="mi">1</span><span class="p">]))</span>

<span class="c1"># Partition the dataset in train + validation sets</span>
<span class="n">X_train</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">y_test</span> <span class="o">=</span> <span class="n">train_test_split</span><span class="p">(</span><span class="n">train</span><span class="p">,</span> <span class="n">y</span><span class="p">,</span> <span class="n">test_size</span> <span class="o">=</span> <span class="mf">0.3</span><span class="p">,</span> <span class="n">random_state</span> <span class="o">=</span> <span class="mi">0</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;X_train : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">X_train</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;X_test : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">X_test</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;y_train : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">y_train</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;y_test : &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">y_test</span><span class="o">.</span><span class="n">shape</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>New number of features : 319
X_train : (1019, 319)
X_test : (437, 319)
y_train : (1019,)
y_test : (437,)
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Standardize numerical features</span>
<span class="n">stdSc</span> <span class="o">=</span> <span class="n">StandardScaler</span><span class="p">()</span>
<span class="n">X_train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="n">numerical_features</span><span class="p">]</span> <span class="o">=</span> <span class="n">stdSc</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">X_train</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="n">numerical_features</span><span class="p">])</span>
<span class="n">X_test</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="n">numerical_features</span><span class="p">]</span> <span class="o">=</span> <span class="n">stdSc</span><span class="o">.</span><span class="n">transform</span><span class="p">(</span><span class="n">X_test</span><span class="o">.</span><span class="n">loc</span><span class="p">[:,</span> <span class="n">numerical_features</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stderr output_text">
<pre>C:\Python\Anaconda3\lib\site-packages\pandas\core\indexing.py:543: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
  self.obj[item] = s
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
<p>在划分测试集和训练集之前时不能做标准化（归一化）的。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Define error measure for official scoring : RMSE</span>
<span class="n">scorer</span> <span class="o">=</span> <span class="n">make_scorer</span><span class="p">(</span><span class="n">mean_squared_error</span><span class="p">,</span> <span class="n">greater_is_better</span> <span class="o">=</span> <span class="kc">False</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">rmse_cv_train</span><span class="p">(</span><span class="n">model</span><span class="p">):</span>
    <span class="n">rmse</span><span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="o">-</span><span class="n">cross_val_score</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">scoring</span> <span class="o">=</span> <span class="n">scorer</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">))</span>
    <span class="k">return</span><span class="p">(</span><span class="n">rmse</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">rmse_cv_test</span><span class="p">(</span><span class="n">model</span><span class="p">):</span>
    <span class="n">rmse</span><span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sqrt</span><span class="p">(</span><span class="o">-</span><span class="n">cross_val_score</span><span class="p">(</span><span class="n">model</span><span class="p">,</span> <span class="n">X_test</span><span class="p">,</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">scoring</span> <span class="o">=</span> <span class="n">scorer</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">))</span>
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
<h3 id="1*-&#19981;&#20570;&#27491;&#21017;&#21270;&#30340;&#32447;&#24615;&#22238;&#24402;">1* &#19981;&#20570;&#27491;&#21017;&#21270;&#30340;&#32447;&#24615;&#22238;&#24402;<a class="anchor-link" href="#1*-&#19981;&#20570;&#27491;&#21017;&#21270;&#30340;&#32447;&#24615;&#22238;&#24402;">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Linear Regression</span>
<span class="n">lr</span> <span class="o">=</span> <span class="n">LinearRegression</span><span class="p">()</span>
<span class="n">lr</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>

<span class="c1"># Look at predictions on training and validation set</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;RMSE on Training set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_train</span><span class="p">(</span><span class="n">lr</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;RMSE on Test set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_test</span><span class="p">(</span><span class="n">lr</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="n">y_train_pred</span> <span class="o">=</span> <span class="n">lr</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_train</span><span class="p">)</span>
<span class="n">y_test_pred</span> <span class="o">=</span> <span class="n">lr</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># Plot residuals</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train_pred</span><span class="p">,</span> <span class="n">y_train_pred</span> <span class="o">-</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test_pred</span><span class="p">,</span> <span class="n">y_test_pred</span> <span class="o">-</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Residuals&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hlines</span><span class="p">(</span><span class="n">y</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span> <span class="n">xmin</span> <span class="o">=</span> <span class="mf">10.5</span><span class="p">,</span> <span class="n">xmax</span> <span class="o">=</span> <span class="mf">13.5</span><span class="p">,</span> <span class="n">color</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot predictions</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train_pred</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test_pred</span><span class="p">,</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Real values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">([</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="p">[</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
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
<pre>RMSE on Training set : 0.38794088514906255
RMSE on Test set : 0.3898435976659904
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
<img src="data:image/png;base64,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yEn7qCqqymmnec/d77zzTo7Xue+++/IfbB4tXbqUVatWcfnl2WsfjTEhoQpTp8IDD8D27fDww/D001C6dMgvHc5xGP8DbvD2A1VNdb9vBL4FmhVEQImJIHLqV2JicK/z22+/0bBhQ+69916aN2/Otm3b6N27N8nJyTRo0IBnnnkma982bdqwbNky0tPTKVu2LAMHDqRJkya0atWK7du3AzB48GBGjBiRtf/AgQNp2bIlderUYcGCBQAcPHiQG264gSZNmtC9e3eSk5Ozkpmnzz//nDp16tCmTRs++eSTrO0LFy6kVatWNGvWjNatW7N+/XoOHz7MM888w/jx42natClTp071up8xJki2bIEuXaBbN6hUCX76CV56qUCSBRRwwhCRWh5vu+AsTJ99nyQRKeG+rgC0BtYURHxpabnbnh9r1qzh7rvv5ueff6ZKlSoMGzaMxYsXs3z5cmbNmsWaNafe8r59+2jbti3Lly+nVatWjBs3zuu5VZWffvqJF198MSv5vPbaa1SsWJHly5czcOBAfv7551OOO3ToEPfccw8zZsxg3rx5pKamZv2sXr16zJ8/n59//pknnniCwYMHU7JkSZ588kl69OjBsmXL6Nq1q9f9jDH5lJEBr74K9evDN984SeKnn+C88wo0jJBVSYnIBKAdUEFEtuJUPXUWkTrACSAFuNfdNxm4V1V7AvWA0SJyAiehDXPXXi5UatasSYsWLbLeT5gwgbfffpv09HRSU1NZs2YN9evXP+mYkiVLcsUVVwBw3nnnMW/ePK/nvv7667P22bx5MwDz589nwIABADRp0oQGDRqcctyaNWuoXbs2NWvWBKBHjx689957AOzdu5fbbruNDRu81gxmCXQ/Y0yAVqyAXr2cBHHZZfDGGxCmsUkhSxiq2t3L5rd97LsY6Om+XgA0ClVckaK0RxFy/fr1jBw5kp9++omyZcty6623eh1/ULx48azXMTExpKenez13iRIlTtkn0IWyfHVlHTRoEJdddhl9+/blt99+89lmEeh+xpgcHD4MzzzjlCaSkmD8eOje3aknDxObSyoC7N+/n4SEBBITE9m2bRszZ84M+jXatGnD5MmTAVi5cqXXKq/69evz66+/smnTJlSVCRMmZP1s3759VKlSBYB33303a3tCQgJpHnV2vvYzxuTC7NnQqBEMGwa33gpr18Itt4Q1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
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
<p>误差似乎随机分布并随机散布在中心线周围，所以我们的模型能够捕获大部分解释性信息。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="2*-&#20570;L2&#27491;&#21017;&#21270;&#65288;&#23725;&#22238;&#24402;&#65289;&#30340;&#32447;&#24615;&#22238;&#24402;">2* &#20570;L2&#27491;&#21017;&#21270;&#65288;&#23725;&#22238;&#24402;&#65289;&#30340;&#32447;&#24615;&#22238;&#24402;<a class="anchor-link" href="#2*-&#20570;L2&#27491;&#21017;&#21270;&#65288;&#23725;&#22238;&#24402;&#65289;&#30340;&#32447;&#24615;&#22238;&#24402;">&#182;</a></h3><p>正则化是处理共线性，从数据中滤除噪声并最终防止过度拟合的非常有用的方法。 正则化背后的概念是引入额外的信息（偏差）来惩罚极端参数权重。</p>
<p>岭回归是L2惩罚模型，我们只需将权重的平方和加到我们的成本函数中。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># 2* Ridge</span>
<span class="n">ridge</span> <span class="o">=</span> <span class="n">RidgeCV</span><span class="p">(</span><span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.03</span><span class="p">,</span> <span class="mf">0.06</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mf">0.3</span><span class="p">,</span> <span class="mf">0.6</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">30</span><span class="p">,</span> <span class="mi">60</span><span class="p">])</span>
<span class="n">ridge</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">alpha</span> <span class="o">=</span> <span class="n">ridge</span><span class="o">.</span><span class="n">alpha_</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best alpha :&quot;</span><span class="p">,</span> <span class="n">alpha</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Try again for more precision with alphas centered around &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">alpha</span><span class="p">))</span>
<span class="n">ridge</span> <span class="o">=</span> <span class="n">RidgeCV</span><span class="p">(</span><span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">6</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">65</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">7</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">75</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">8</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">85</span><span class="p">,</span> 
                          <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">9</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">95</span><span class="p">,</span> <span class="n">alpha</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.05</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.1</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.15</span><span class="p">,</span>
                          <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.25</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.3</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.35</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.4</span><span class="p">],</span> 
                <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">ridge</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">alpha</span> <span class="o">=</span> <span class="n">ridge</span><span class="o">.</span><span class="n">alpha_</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best alpha :&quot;</span><span class="p">,</span> <span class="n">alpha</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Ridge RMSE on Training set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_train</span><span class="p">(</span><span class="n">ridge</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Ridge RMSE on Test set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_test</span><span class="p">(</span><span class="n">ridge</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="n">y_train_rdg</span> <span class="o">=</span> <span class="n">ridge</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_train</span><span class="p">)</span>
<span class="n">y_test_rdg</span> <span class="o">=</span> <span class="n">ridge</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># Plot residuals</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train_rdg</span><span class="p">,</span> <span class="n">y_train_rdg</span> <span class="o">-</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test_rdg</span><span class="p">,</span> <span class="n">y_test_rdg</span> <span class="o">-</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression with Ridge regularization&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Residuals&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hlines</span><span class="p">(</span><span class="n">y</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span> <span class="n">xmin</span> <span class="o">=</span> <span class="mf">10.5</span><span class="p">,</span> <span class="n">xmax</span> <span class="o">=</span> <span class="mf">13.5</span><span class="p">,</span> <span class="n">color</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot predictions</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train_rdg</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test_rdg</span><span class="p">,</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression with Ridge regularization&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Real values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">([</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="p">[</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot important coefficients</span>
<span class="n">coefs</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">ridge</span><span class="o">.</span><span class="n">coef_</span><span class="p">,</span> <span class="n">index</span> <span class="o">=</span> <span class="n">X_train</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Ridge picked &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coefs</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; features and eliminated the other &quot;</span> <span class="o">+</span>  \
      <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coefs</span> <span class="o">==</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; features&quot;</span><span class="p">)</span>
<span class="n">imp_coefs</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">coefs</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">),</span>
                     <span class="n">coefs</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">tail</span><span class="p">(</span><span class="mi">10</span><span class="p">)])</span>
<span class="n">imp_coefs</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span> <span class="o">=</span> <span class="s2">&quot;barh&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Coefficients in the Ridge Model&quot;</span><span class="p">)</span>
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
<pre>Best alpha : 30.0
Try again for more precision with alphas centered around 30.0
Best alpha : 24.0
Ridge RMSE on Training set : 0.11540572328450797
Ridge RMSE on Test set : 0.11642721377799559
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
<img src="data:image/png;base64,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795e94uOjgYgOTmZzp07Ox7bvRmxu6FDh3LixImM5Xbt2nH48GFfkp4t6el1cvjwYYYPH+738yoVCEN2DGfowWHnPYYfysZ32BirD8Xll1ujy774IqxcGbbBAjRgBFyXLl346quvMq376quv6NLF08gp5ytfvjyTJk3K8fndA8bUqVMpWbJkjo+XUxowVDiJijnrcf1ZPK8/z6ZN0KoVPPCANWDgqlUwaBDYw/aEKw0YLoYfGs6wQ8POe2TrrsJN586dmTJlCqdPnwZg+/btJCcn07Rp04y+EfXr1+eKK67INJx4uu3bt5OQkADAyZMnufPOO6lTpw533HEHJ0+ezNiuV69eGcOjv/iiNcXIe++9R3JyMtdeey3XXnstAFWqVGH//v0AvPPOOyQkJJCQkJAxPPr27dupWbMmPXr0oHbt2rRu3TrTedJt27aNxo0b06BBA55//vmM9U7XNGDAALZs2UJiYiL9+vXz6dqVCkVee3efOQOvvmoN67FsGYwYYRVB5ZPOp1qH4cLp7sHnuwoP4uPjadiwIdOmTaNDhw589dVX3HHHHYgIUVFRTJ48mdjYWPbv389VV11F+/btHQcA/OijjyhWrBirV69m9erV1K9fP+O1V155hVKlSpGWlkarVq1YvXo1jz/+OO+88w6zZ8+mdOnSmY61bNkyPv30UxYvXowxhkaNGtG8eXPi4uLYtGkT48aNY/To0dx+++18/fXX3H333Zn279OnD7169eLee+/lww8/zFjvdE1Dhgxh7dq1GXNwpKamZuvalQqEmJjc96/I2H/RIqup7Nq1VmX2sGFQvnyu0xhKNIeRB1yLpVyLo4wxPPvss9SpU4frrruOv//+mz179jgeZ968eRk/3HXq1KGOS2/QCRMmUL9+ferVq8e6des8Di7oasGCBXTs2JHixYsTHR1Np06dMoZLr1q1KomJiUDmIdJd/frrrxnXcc8992Ss9/WasnvtSgWCP3pux3AUHnsMrr4aDh2ymslOnJjvggVoDiNP3HLLLTz55JMsX76ckydPZuQMxo4dy759+1i2bBmRkZFUqVLF47DmrjzdgW/bto233nqLJUuWEBcXR7du3bI8jrcxxIq4lLNGRER4LJJySouv15STa1cq1NzM9wynN3yYDI88Aq+84v8pOkOI5jDyQHR0NC1atOCBBx7IVNl95MgRLrzw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
"
>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Ridge picked 316 features and eliminated the other 3 features
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

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>由于我们已经添加了正则化，因此我们得到了更好的RMSE结果。 训练和测试结果之间的微小差异表明我们消除了大部分过度拟合。 在视觉上，图表似乎证实了这个想法。</p>
<p>Ridge几乎使用了所有现有特征。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="3*-&#20570;-L1&#33539;&#25968;&#27491;&#21017;&#21270;&#65288;Lasso&#22238;&#24402;&#65289;&#30340;&#32447;&#24615;&#22238;&#24402;">3* &#20570; L1&#33539;&#25968;&#27491;&#21017;&#21270;&#65288;Lasso&#22238;&#24402;&#65289;&#30340;&#32447;&#24615;&#22238;&#24402;<a class="anchor-link" href="#3*-&#20570;-L1&#33539;&#25968;&#27491;&#21017;&#21270;&#65288;Lasso&#22238;&#24402;&#65289;&#30340;&#32447;&#24615;&#22238;&#24402;">&#182;</a></h3><p>LASSO代表<em>最小绝对收缩和选择算子</em>。 它是一种替代正则化方法，其中我们简单地用权重的绝对值之和替换权重的平方。 与L2正则化相反，L1正则化产生稀疏特征向量：大多数特征权重将为零。 如果我们的高维数据集具有许多不相关的特征，则稀疏性在实践中可能是有用的。</p>
<p>我们可以猜测它应该比L2更有效率。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># 3* Lasso</span>
<span class="n">lasso</span> <span class="o">=</span> <span class="n">LassoCV</span><span class="p">(</span><span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.0001</span><span class="p">,</span> <span class="mf">0.0003</span><span class="p">,</span> <span class="mf">0.0006</span><span class="p">,</span> <span class="mf">0.001</span><span class="p">,</span> <span class="mf">0.003</span><span class="p">,</span> <span class="mf">0.006</span><span class="p">,</span> <span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.03</span><span class="p">,</span> <span class="mf">0.06</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> 
                          <span class="mf">0.3</span><span class="p">,</span> <span class="mf">0.6</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span> 
                <span class="n">max_iter</span> <span class="o">=</span> <span class="mi">50000</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">lasso</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">alpha</span> <span class="o">=</span> <span class="n">lasso</span><span class="o">.</span><span class="n">alpha_</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best alpha :&quot;</span><span class="p">,</span> <span class="n">alpha</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Try again for more precision with alphas centered around &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">alpha</span><span class="p">))</span>
<span class="n">lasso</span> <span class="o">=</span> <span class="n">LassoCV</span><span class="p">(</span><span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">6</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">65</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">7</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">75</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">8</span><span class="p">,</span> 
                          <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">85</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">9</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">95</span><span class="p">,</span> <span class="n">alpha</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.05</span><span class="p">,</span> 
                          <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.1</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.15</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.25</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.3</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.35</span><span class="p">,</span> 
                          <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.4</span><span class="p">],</span> 
                <span class="n">max_iter</span> <span class="o">=</span> <span class="mi">50000</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">lasso</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">alpha</span> <span class="o">=</span> <span class="n">lasso</span><span class="o">.</span><span class="n">alpha_</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best alpha :&quot;</span><span class="p">,</span> <span class="n">alpha</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Lasso RMSE on Training set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_train</span><span class="p">(</span><span class="n">lasso</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Lasso RMSE on Test set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_test</span><span class="p">(</span><span class="n">lasso</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="n">y_train_las</span> <span class="o">=</span> <span class="n">lasso</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_train</span><span class="p">)</span>
<span class="n">y_test_las</span> <span class="o">=</span> <span class="n">lasso</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># Plot residuals</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train_las</span><span class="p">,</span> <span class="n">y_train_las</span> <span class="o">-</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test_las</span><span class="p">,</span> <span class="n">y_test_las</span> <span class="o">-</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression with Lasso regularization&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Residuals&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hlines</span><span class="p">(</span><span class="n">y</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span> <span class="n">xmin</span> <span class="o">=</span> <span class="mf">10.5</span><span class="p">,</span> <span class="n">xmax</span> <span class="o">=</span> <span class="mf">13.5</span><span class="p">,</span> <span class="n">color</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot predictions</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train_las</span><span class="p">,</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test_las</span><span class="p">,</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression with Lasso regularization&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Real values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">([</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="p">[</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot important coefficients</span>
<span class="n">coefs</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">lasso</span><span class="o">.</span><span class="n">coef_</span><span class="p">,</span> <span class="n">index</span> <span class="o">=</span> <span class="n">X_train</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Lasso picked &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coefs</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; features and eliminated the other &quot;</span> <span class="o">+</span>  \
      <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coefs</span> <span class="o">==</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; features&quot;</span><span class="p">)</span>
<span class="n">imp_coefs</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">coefs</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">),</span>
                     <span class="n">coefs</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">tail</span><span class="p">(</span><span class="mi">10</span><span class="p">)])</span>
<span class="n">imp_coefs</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span> <span class="o">=</span> <span class="s2">&quot;barh&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Coefficients in the Lasso Model&quot;</span><span class="p">)</span>
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
<pre>Best alpha : 0.0006
Try again for more precision with alphas centered around 0.0006
Best alpha : 0.0006
Lasso RMSE on Training set : 0.11411150837458059
Lasso RMSE on Test set : 0.11583213221750707
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY0AAAEWCAYAAACaBstRAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJztnXm8HFW1778/woFAcg6EGQJJAAEJMSThgCJTUGRSBpUrBJBRosQBH8Ml7zKI8HhGAU1UcoGrKEguiNwncCVcBpVR0CSQQAhiAiQSEkgIGU4IQw6s90dVn1T6dHVXj9XD+n4+/emuql271q6q3mvvtfZeW2aG4ziO4yRhg7QFcBzHcRoHVxqO4zhOYlxpOI7jOIlxpeE4juMkxpWG4ziOkxhXGo7jOE5iXGnUAZIOkvRS2nI0KpJOkfRgvV5f0mhJC2spU6MjaYgkk7RhiedX5T+V9rtWD8jnadQOSfOBr5nZw2nL4lQPSQbsZmbzwu3RwG1mtmPC8x8J0/+iakLWOZKGAK8CbWbW3aoy1CPe02hhkrTiSm3p1So/Jx0UUJf1h79j1aUuH3qrkW2+kDRf0oWSnpO0UtJvJfWNHP+CpJmSVkj6i6ThkWPjJb0sqUvSHElfjBw7Q9KTkn4i6W3gihyyXCHpLkm3SVoFnCFpg0i+yyTdKWmLyDmnSVoQHrsslP+wUvKT1DdMuyws3zRJ20bkfyUs26uSTonsfyIiz6fD81aG35+OHHtE0lXhfeiS9KCkrWKey6OSvhz+PjA0lxwdbh8maWb29SU9Fp4+S9JqSSdG8rtA0hJJiyWdGftC5EHS7yS9EZbtMUl7RY4dHT7zLkmvS7ow3L+VpD+E9/NtSY9nKnxJe4b3ZIWkFyQdm+faj0i6WtKTwBpgF0mbSfplWKbXJf0fSX3C9H0kXSfprfB5fUsRk1P0PQm3r5B0W8y1z5T0Yli2VyR9PXJstKSFki6W9AbwK0X+U5JODJ9F5vO+gt4ckj4v6VlJqyS9JumKyGUzz3JFeN7+1XrXGglXGvXLV4AjgZ2B4cAZAJJGATcDXwe2BG4E7pW0cXjey8BBwGbA94HbJG0fyfeTwCvANsDVMdc+DrgL2ByYAnwHOB44BNgBWA5cH8ozFJgMnAJsH153YKn5AaeHeewUlu8bwLuS+gE/BY4ys3bg08DMbMFD5XNfmHZL4MfAfZK2jCQ7GTgzvAcbARfG3IdHgdHh74MJ7tshke1Hs08ws4PDn3ubWX8z+224vR3r7s3ZwPWSBsRcNx/3A7uFsj9DcD8z/BL4enh/hgF/CvdfACwEtga2Bf4NMEltwH8DD4b5fRuYImmPPNf/KjAWaAcWALcA3cDHgJHA4cDXwrTnAEcBI4BRBM+8VJYAXwA6CJ7dT8L/QobtgC2AwaF8PZjZb8Nn0Z/gfXsFuD08/A5wGsG7+XngXEkZOTPPcvPw/Kei+Vb4XWsYXGnULz81s0Vm9jbBH3tEuP8c4EYz+6uZfWhmtwDvA58CMLPfhed9FFZYc4H9IvkuMrOfmVm3mb0bc+2nzOzuMI93CRTUJWa20MzeJ+ihnBC2GE8A/tvMnjCzD4DLgWxHWTH5rSX4A34sLN8MM1sV5vMRMEzSJma22MxeyCH754G5ZvabsIy3A38Hjomk+ZWZ/SOU5c7Ivc3mUdZXEj+IbB9CDqWRh7XAlWa21symAquBfJVzTszsZjPrity3vSVtFrnGUEkdZrbczJ6J7N8eGBxe/3ELnJmfAvoDE8zsAzP7E/AHYEweEX5tZi+ENv4tCJTCd83sHTNbAvwEOClM+xVgUviclwMTii1vpNz3mdnLFvAogaI7KJLkI+B7ZvZ+3Hsd9q7+E3jEzG4M833EzJ4P383nCJTJIbnOz0El37WGwZVG/fJG5Pcagj83BC2pC0JzwgpJKwha5TtAj6loZuTYMCDaJX4twbWz0wwGfh/J80XgQ4JW6w7R9Ga2BlhWRn6/AR4A7pC0SNKPJLWZ2TvAiQQ9j8WS7pP08Ryy70DQAo6ygPV7P3H3NpungN0VmMdGALcCO4Umhv1YZ75IwrIsZ2q+6+YkNPdMUGDWWwXMDw9lnu+XgaOBBQpMa/uH+68B5gEPhqad8eH+HYDXzOyjyGWy71U20Wc5GGgjeB6ZZ3kjQau6J/+Yc4tC0lGSng7NaysIyhl9r5ea2XsFsrmaoIf0nUi+n5T0Z0lLJa0keL+SmpAq+a41DK40Go/XgKvNbPPIZ1Mzu13SYOA/gG8BW5rZ5sBsQJHzkwyXy07zGoFZKHrNvmb2OrAY6BkVJGkTgp5CSfmFLeHvm9lQAhPUFwjMB5jZA2b2OYJW89/DsmaziKAyizIIeD1BudcXOlCAM4DzgNlhT+ovwPnAy2b2VrF5lsnJBKa+wwhMXUPC/QrlnWZmxxFU2ncTtGwJeyYXmNkuBK3g8yV9luBe7aT1HdqF7lX0Wb5G0MvdKvIcO8ws42dZ790gaNxEeQfYNLK9Xa4LhqbX/wKuBbYN3+upFPFeSzqJoAd1gpmtjRz6T+BeYCcz2wy4IZJvof9Kxd61RsKVRu1pU+DszXyKHenxH8A3whaSJPULnXntQD+CF30pBM5Dgp5GudwAXB0qJSRtLem48NhdwDGhQ3AjAj+KYvIpmJ+kQyV9QoEzdRWBaeVDSdtKOjb0bbxPYN75MEfeUwl6BydL2lCBI3oogdmlFB4lUMIZU9QjWdu5eBPYpcTrZdgw6z1pI2glv0/Qk9sU+L+ZxJI2UjCHYLOwUlxFeH8UDJz4mCRF9n8I/JWg4v5XSW0KhgYfA9yRREAzW0xgJrpOUoeCAQ67SsqYd+4EzpM0UNLmwMVZWcwETgqv3Ulg6szFRsDGBO91t6SjCHwniZA0EvgZcLyZLc063A68bWbvSdqPQDFnWEpg9op7lpV+1xoCVxq1ZyrwbuRzRTEnm9l0Ar/GzwkcyPMIneRmNge4jsCs8ibwCeDJCsg8iaA19qCkLuBpAoc6oV/h2wQVzWKgi8Bp+X4p+RG0Nu8iqNxeJKicbyN4Vy8gaN29TWB3HpedsZktI+idXEBQuf4r8IUyegWPElQsj8Vs5+IK4JbQZPOVEq/776z/nvyKwDy2gKAlO4fgvkX5KjA/NF19Azg13L8b8DCBon0KmBza8j8AjiXwS7xFMKDhNDP7exFynkZQqc8heB/vIugJQtDAeRB4DniW4N3vZp2yvwzYNTzv+wSt/l6YWReBSenOMO3JBO9PUo4DBgBPaN0IqvvDY+OAK8P38PLwGpnrriEwaT0ZPstPZclV6XetIfDJfU5FkdQfWEEwue3VtOVx6oewh3CDmWWbdJwGwnsaTtlIOkbSpqHp6FrgedY5aZ0WRdImCuaObChpIPA94Pdpy+WUhysNpxIcR2A2WkRgCjnJvAvrBL6t7xOYlJ4lMDdenqpETtm4ecpxHMdJjPc0HMdxnMQ0XWCvrbbayoYMGZK2GI7jOA3FjBkz3jKzrQulazqlMWTIEKZPn562GI7jOA2FpOzZ7Tlx85TjOI6TGFcajuM4TmJcaTiO4ziJaTqfRi7Wrl3LwoULee+9QkEwnXqjb9++7LjjjrS1taUtiuM4tIjSWLhwIe3t7QwZMoQgZpvTCJgZy5YtY+HChey8885pi+M4Di1innrvvffYcsstXWE0GJLYcsstvYfoOHVESygNwBVGg+LPzXHqi5ZRGo7jOE75uNKoAcuWLWPEiBGMGDGC7bbbjoEDB/Zsf/DBB4nyOPPMM3nppZfyprn++uuZMmVKJURej4cffpjjjz8+b5pnnnmG//mf/6n4tZuJjg6Qen86OtKWzHGS0xKO8LTZcsstmTlzJgBXXHEF/fv358ILL1wvjZlhZmywQW49/qtf/argdb75zW+WL2yJPPPMM8yePZsjjzwyNRnqna6u4vY7Tj3iPY0satkanDdvHsOGDeMb3/gGo0aNYvHixYwdO5bOzk722msvrrzyyp60Bx54IDNnzqS7u5vNN9+c8ePHs/fee7P//vuzZMkSAC699FImTpzYk378+PHst99+7LHHHvzlL38B4J133uHLX/4ye++9N2PGjKGzs7NHoUW577772GOPPTjwwAO55557evY//fTT7L///owcOZIDDjiAuXPn8u6773LllVcyZcoURowYwV133ZUzneM4jY8rjSxq3RqcM2cOZ599Ns8++ywDBw5kwoQJTJ8+nVmzZvHQQw8xZ86cXuesXLmSQw45hFmzZrH//vtz880358zbzPjb3/7GNddc06OAfvazn7Hddtsxa9Ysxo8fz7PPPtvrvDVr1vD1r3+dqVOn8vjjj7No0aKeY3vuuSdPPPEEzz77LJdddhmXXnopm2yyCZdffjmnnHIKM2fO5IQTTsiZznGcxsfNUymz6667su+++/Zs33777fzyl7+ku7ubRYsWMWfOHIYOHbreOZtssglHHXUUAPvssw+PP/54zry/9KUv9aSZP38+AE888QQXX3wxAHvvvTd77bVXr/PmzJnD7rvvzq677grAKaecwq233grAihUrOO2003j55ZfzlitpOsdxGgvvaaRMv379en7PnTuXSZMm8ac//YnnnnuOI488MucchY022qjnd58+feju7s6Z98Ybb9wrTdJFt+KGul5yySUcccQRzJ49m7vvvjt2DkXSdI7jNBauNOqIVatW0d7eTkdHB4sXL+aBBx6o+DUOPPBA7rzzTgCef/75nOavoUOH8o9//INXX30VM+P222/vObZy5UoGDhwIwK9//eue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
"
>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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yUqvP3v27GHYsGEhP64xoTR40zCG7Bqa4zF091Be3JyP366q04fizDOd0WWffBKWLYvbYAEWMMKuR48efPLJJzmWffLJJ/To4WvklONVrVqV8ePH5/v43gFj8uTJlCtXLt/7yy8LGCYeJCYf9bm8ZJLv5X6tXQsdOsBttzkDBi5fDoMGgTtsT7yygOFh2O5hDN099LjHsN35v9B169aNSZMmcfjwYQA2btxIWloabdq0ye4b0axZM84666wcw4ln2bhxIw0bNgTg4MGDXHvttTRq1IhrrrmGgwcPZq/Xu3fv7OHRn3zSmWLk9ddfJy0tjQsuuIALLrgAgJo1a7Jjxw4AXn31VRo2bEjDhg2zh0ffuHEj9erVo2fPnjRo0ICOHTvmOE6W3377jVatWtG8eXMef/zx7OX+zmnAgAGsX7+eJk2a8PDDDwd07sbEmjx7eB85As895wzrsXgxvP22UwRVSDqfWh2Gh6P4vovwtzwQFStWpEWLFnzzzTd07dqVTz75hGuuuQYRITExkYkTJ5KSksKOHTs455xz6NKli98BAN966y1Kly7NihUrWLFiBc2aNct+79lnn6VChQpkZmbSoUMHVqxYwX333cerr77KzJkzqVSpUo59LV68mPfff58FCxagqrRs2ZK2bdtSvnx51q5dy+jRo3nnnXfo3r07n376KTfccEOO7fv27Uvv3r256aabePPNN7OX+zunwYMHs3Llyuw5ODIyMoI6d2PCJTk58IrvXPtrzJ/vNJVdudKpzB46FKpWDVk6Y4HlMCLAs1jKszhKVXn00Udp1KgRF154IX/88Qd//fWX3/3Mnj07+8LdqFEjGnn0Bh07dizNmjWjadOmrFq1yufggp7mzp3LFVdcQZkyZUhKSuLKK6/MHi69Vq1aNGnSBMg5RLqn77//Pvs8brzxxuzlgZ5TsOduTLjs2+dUN+R3lKRk9vE698K558Lu3U4z2XHjCl2wAMthRMTll1/OAw88wJIlSzh48GB2zmDUqFFs376dxYsXk5CQQM2aNX0Oa+7J1x34b7/9xssvv8zChQspX748t9xyS577yW0MsZIe5azFihXzWSTlLy2BnlN+zt2YWHMZXzCMPlQlDe6+G559NsIdOyLLchgRkJSURLt27bjttttyVHbv3buXk046iYSEBGbOnMmmTZty3c/555/PqFGjAFi5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
"
>
</div>

</div>

<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>Lasso picked 111 features and eliminated the other 208 features
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

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>RMSE结果在训练和测试集上都变得更好。最有趣的是，Lasso只使用了三分之一的特征。 另一个有趣的现象：它似乎对“Neighborhood”这个变量很看重，无论是积极的还是消极的。 直观地说，在同一个城市，房价从一个街区到另一个街区变化很大。</p>
<p>与其他功能相比，“MSZoning_C（all）”（房屋所在区域）功能似乎具有不成比例的影响。 它被定义为一般分区分类：商业。 对我来说，把你的房子放在一个大多数商业区是一件非常可怕的事情，这似乎有点奇怪。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="4*-&#20570;-L1&#21644;L2&#27491;&#21017;&#21270;&#30340;&#32447;&#24615;&#22238;&#24402;">4* &#20570; L1&#21644;L2&#27491;&#21017;&#21270;&#30340;&#32447;&#24615;&#22238;&#24402;<a class="anchor-link" href="#4*-&#20570;-L1&#21644;L2&#27491;&#21017;&#21270;&#30340;&#32447;&#24615;&#22238;&#24402;">&#182;</a></h3><p>ElasticNet是Ridge和Lasso回归的折衷。 它有一个L1惩罚来产生稀疏性和L2惩罚来克服Lasso的一些限制，例如变量的数量（Lasso不能选择比观察更多的特征，但不管怎么说都不是这样）。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># 4* ElasticNet</span>
<span class="n">elasticNet</span> <span class="o">=</span> <span class="n">ElasticNetCV</span><span class="p">(</span><span class="n">l1_ratio</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.1</span><span class="p">,</span> <span class="mf">0.3</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.6</span><span class="p">,</span> <span class="mf">0.7</span><span class="p">,</span> <span class="mf">0.8</span><span class="p">,</span> <span class="mf">0.85</span><span class="p">,</span> <span class="mf">0.9</span><span class="p">,</span> <span class="mf">0.95</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span>
                          <span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.0001</span><span class="p">,</span> <span class="mf">0.0003</span><span class="p">,</span> <span class="mf">0.0006</span><span class="p">,</span> <span class="mf">0.001</span><span class="p">,</span> <span class="mf">0.003</span><span class="p">,</span> <span class="mf">0.006</span><span class="p">,</span> 
                                    <span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.03</span><span class="p">,</span> <span class="mf">0.06</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mf">0.3</span><span class="p">,</span> <span class="mf">0.6</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">6</span><span class="p">],</span> 
                          <span class="n">max_iter</span> <span class="o">=</span> <span class="mi">100000</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">elasticNet</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="n">alpha</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">alpha_</span>
<span class="n">ratio</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">l1_ratio_</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best l1_ratio :&quot;</span><span class="p">,</span> <span class="n">ratio</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best alpha :&quot;</span><span class="p">,</span> <span class="n">alpha</span> <span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Try again for more precision with l1_ratio centered around &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">ratio</span><span class="p">))</span>
<span class="n">elasticNet</span> <span class="o">=</span> <span class="n">ElasticNetCV</span><span class="p">(</span><span class="n">l1_ratio</span> <span class="o">=</span> <span class="p">[</span><span class="n">ratio</span> <span class="o">*</span> <span class="o">.</span><span class="mi">85</span><span class="p">,</span> <span class="n">ratio</span> <span class="o">*</span> <span class="o">.</span><span class="mi">9</span><span class="p">,</span> <span class="n">ratio</span> <span class="o">*</span> <span class="o">.</span><span class="mi">95</span><span class="p">,</span> <span class="n">ratio</span><span class="p">,</span> <span class="n">ratio</span> <span class="o">*</span> <span class="mf">1.05</span><span class="p">,</span> <span class="n">ratio</span> <span class="o">*</span> <span class="mf">1.1</span><span class="p">,</span> <span class="n">ratio</span> <span class="o">*</span> <span class="mf">1.15</span><span class="p">],</span>
                          <span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="mf">0.0001</span><span class="p">,</span> <span class="mf">0.0003</span><span class="p">,</span> <span class="mf">0.0006</span><span class="p">,</span> <span class="mf">0.001</span><span class="p">,</span> <span class="mf">0.003</span><span class="p">,</span> <span class="mf">0.006</span><span class="p">,</span> <span class="mf">0.01</span><span class="p">,</span> <span class="mf">0.03</span><span class="p">,</span> <span class="mf">0.06</span><span class="p">,</span> <span class="mf">0.1</span><span class="p">,</span> <span class="mf">0.3</span><span class="p">,</span> <span class="mf">0.6</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">6</span><span class="p">],</span> 
                          <span class="n">max_iter</span> <span class="o">=</span> <span class="mi">100000</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">elasticNet</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="k">if</span> <span class="p">(</span><span class="n">elasticNet</span><span class="o">.</span><span class="n">l1_ratio_</span> <span class="o">&gt;</span> <span class="mi">1</span><span class="p">):</span>
    <span class="n">elasticNet</span><span class="o">.</span><span class="n">l1_ratio_</span> <span class="o">=</span> <span class="mi">1</span>    
<span class="n">alpha</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">alpha_</span>
<span class="n">ratio</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">l1_ratio_</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best l1_ratio :&quot;</span><span class="p">,</span> <span class="n">ratio</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best alpha :&quot;</span><span class="p">,</span> <span class="n">alpha</span> <span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Now try again for more precision on alpha, with l1_ratio fixed at &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">ratio</span><span class="p">)</span> <span class="o">+</span> 
      <span class="s2">&quot; and alpha centered around &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">alpha</span><span class="p">))</span>
<span class="n">elasticNet</span> <span class="o">=</span> <span class="n">ElasticNetCV</span><span class="p">(</span><span class="n">l1_ratio</span> <span class="o">=</span> <span class="n">ratio</span><span class="p">,</span>
                          <span class="n">alphas</span> <span class="o">=</span> <span class="p">[</span><span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">6</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">65</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">7</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">75</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">8</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">85</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">9</span><span class="p">,</span> 
                                    <span class="n">alpha</span> <span class="o">*</span> <span class="o">.</span><span class="mi">95</span><span class="p">,</span> <span class="n">alpha</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.05</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.1</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.15</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.25</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.3</span><span class="p">,</span> 
                                    <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.35</span><span class="p">,</span> <span class="n">alpha</span> <span class="o">*</span> <span class="mf">1.4</span><span class="p">],</span> 
                          <span class="n">max_iter</span> <span class="o">=</span> <span class="mi">100000</span><span class="p">,</span> <span class="n">cv</span> <span class="o">=</span> <span class="mi">10</span><span class="p">)</span>
<span class="n">elasticNet</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">X_train</span><span class="p">,</span> <span class="n">y_train</span><span class="p">)</span>
<span class="k">if</span> <span class="p">(</span><span class="n">elasticNet</span><span class="o">.</span><span class="n">l1_ratio_</span> <span class="o">&gt;</span> <span class="mi">1</span><span class="p">):</span>
    <span class="n">elasticNet</span><span class="o">.</span><span class="n">l1_ratio_</span> <span class="o">=</span> <span class="mi">1</span>    
<span class="n">alpha</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">alpha_</span>
<span class="n">ratio</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">l1_ratio_</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best l1_ratio :&quot;</span><span class="p">,</span> <span class="n">ratio</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Best alpha :&quot;</span><span class="p">,</span> <span class="n">alpha</span> <span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;ElasticNet RMSE on Training set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_train</span><span class="p">(</span><span class="n">elasticNet</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;ElasticNet RMSE on Test set :&quot;</span><span class="p">,</span> <span class="n">rmse_cv_test</span><span class="p">(</span><span class="n">elasticNet</span><span class="p">)</span><span class="o">.</span><span class="n">mean</span><span class="p">())</span>
<span class="n">y_train_ela</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_train</span><span class="p">)</span>
<span class="n">y_test_ela</span> <span class="o">=</span> <span class="n">elasticNet</span><span class="o">.</span><span class="n">predict</span><span class="p">(</span><span class="n">X_test</span><span class="p">)</span>

<span class="c1"># Plot residuals</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train_ela</span><span class="p">,</span> <span class="n">y_train_ela</span> <span class="o">-</span> <span class="n">y_train</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test_ela</span><span class="p">,</span> <span class="n">y_test_ela</span> <span class="o">-</span> <span class="n">y_test</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression with ElasticNet regularization&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Residuals&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">hlines</span><span class="p">(</span><span class="n">y</span> <span class="o">=</span> <span class="mi">0</span><span class="p">,</span> <span class="n">xmin</span> <span class="o">=</span> <span class="mf">10.5</span><span class="p">,</span> <span class="n">xmax</span> <span class="o">=</span> <span class="mf">13.5</span><span class="p">,</span> <span class="n">color</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot predictions</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_train</span><span class="p">,</span> <span class="n">y_train_ela</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;blue&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Training data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">scatter</span><span class="p">(</span><span class="n">y_test</span><span class="p">,</span> <span class="n">y_test_ela</span><span class="p">,</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;lightgreen&quot;</span><span class="p">,</span> <span class="n">marker</span> <span class="o">=</span> <span class="s2">&quot;s&quot;</span><span class="p">,</span> <span class="n">label</span> <span class="o">=</span> <span class="s2">&quot;Validation data&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Linear regression with ElasticNet regularization&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Predicted values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Real values&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">(</span><span class="n">loc</span> <span class="o">=</span> <span class="s2">&quot;upper left&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">([</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="p">[</span><span class="mf">10.5</span><span class="p">,</span> <span class="mf">13.5</span><span class="p">],</span> <span class="n">c</span> <span class="o">=</span> <span class="s2">&quot;red&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>

<span class="c1"># Plot important coefficients</span>
<span class="n">coefs</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">elasticNet</span><span class="o">.</span><span class="n">coef_</span><span class="p">,</span> <span class="n">index</span> <span class="o">=</span> <span class="n">X_train</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;ElasticNet picked &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coefs</span> <span class="o">!=</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; features and eliminated the other &quot;</span> <span class="o">+</span>  <span class="nb">str</span><span class="p">(</span><span class="nb">sum</span><span class="p">(</span><span class="n">coefs</span> <span class="o">==</span> <span class="mi">0</span><span class="p">))</span> <span class="o">+</span> <span class="s2">&quot; features&quot;</span><span class="p">)</span>
<span class="n">imp_coefs</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">concat</span><span class="p">([</span><span class="n">coefs</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">10</span><span class="p">),</span>
                     <span class="n">coefs</span><span class="o">.</span><span class="n">sort_values</span><span class="p">()</span><span class="o">.</span><span class="n">tail</span><span class="p">(</span><span class="mi">10</span><span class="p">)])</span>
<span class="n">imp_coefs</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">kind</span> <span class="o">=</span> <span class="s2">&quot;barh&quot;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s2">&quot;Coefficients in the ElasticNet Model&quot;</span><span class="p">)</span>
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
<pre>Best l1_ratio : 1.0
Best alpha : 0.0006
Try again for more precision with l1_ratio centered around 1.0
Best l1_ratio : 1.0
Best alpha : 0.0006
Now try again for more precision on alpha, with l1_ratio fixed at 1.0 and alpha centered around 0.0006
Best l1_ratio : 1.0
Best alpha : 0.0006
ElasticNet RMSE on Training set : 0.11411150837458059
ElasticNet RMSE on Test set : 0.11583213221750707
</pre>
</div>
</div>

<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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jB49mltuuSU2XTuzfDmY9f4sX561ZI6TnJZbI7yrq8vyF2F69tln2W233RKd39lZ2Ond0dEaf+41a9awZs0a+vfvz9y5cznkkEOYO3cuffs2rnurnOfnOE5lSJppZl2l0jVuTZERraAYirFixQoOOugg1qxZg5nxs5/9rKEVhtN4TF06ldWs7rW/H/2YMGhCBhI59cRrizZjk002YebMmVmL4TQxhRRGsf1Oa+E+DcdxHCcxrjQcx3GcxLjScBzHcRLjPg2nhzfWvIHRezSdEFv23TIDiRzHaTS8p1EHxo0b12ui3uTJk5kwofhIk4EDBwKwcOFCjjnmmNi884cY5zN58mRWrlzZs33EEUfw9ttv90pXSGEU2x8nbxxvv/02U6dOTZSX07j0o/B67XH7ndbCexp1YPz48dx0000ceuihPftuuukmLr/88kTnb7vtttxyyy0VX3/y5MmccMIJbLTRRgDceeedFedVDTmlUUpZOo1LMI+p9/NrlXlMTmky7WlIOkzSc5KelzQxJs0XJc2R9Iyk/1trmaYuncqUpVN6faYurbyFfMwxx/D73/+e9957D4B58+axcOFC9t133555E2PGjOEjH/nIOmHIc8ybN48RI0YAsGrVKo477jhGjhzJsccey6pVq3rSnXHGGT1h1b///e8D8JOf/ISFCxdy4IEHcuCBBwIwbNgw3nzzTQB+/OMfM2LECEaMGME1U64B4OV5L7PfR/bje1/7HvvvsT/HHr7udXK89NJL7LPPPuy1116cf/75PfvjyjRx4kReeOEFRo0axdlnn52o7E5j4WuCOD2L/9T7A/QBXgA+BKwPzAaG56XZGXgCGBRub1kq3z333NPymTNnTq99cUx+a3LspxqOOOIIu/XWW83M7JJLLrGzzjrLzMxWr15ty5YtMzOzxYsX24477mgffPCBmZkNGDDAzMxeeukl23333c3M7IorrrCTTz7ZzMxmz55tffr0senTp5uZ2ZIlS8zMbM2aNXbAAQfY7Nmzzcxs++23t8WLF/fIktueMWOGjRgxwlasWGHd3d22y/Bd7J7H7rHH5j5mffr0sXun32uvrX7NjjzmSPvBD26w6dPNpk83mzkzyOfII4+06667zszMrrzyyh5548oULUepskcp5/k5taVwIJTg4zQ3wAxLUHdn2dPYG3jezF40s38CNwFH5aU5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
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

<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>ElasticNet picked 111 features and eliminated the other 208 features
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

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>这里ElasticNet使用的最佳L1比率等于1，这意味着它与我们之前使用的Lasso回归量完全相同（并且它等于0，它将完全等于我们的Ridge回归量）。 该模型不需要任何L2正则化来克服任何潜在的L1缺点。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Note : 我删掉了 "MSZoning_C (all)"这个特征, 导致CV得分略差, 但LB得分稍好一些。</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="&#32467;&#35770;">&#32467;&#35770;<a class="anchor-link" href="#&#32467;&#35770;">&#182;</a></h3><p>花费时间和精力来准备数据集并正则化可以得到不错的分数，会优于一些公共脚本，这些脚本在历史的Kaggle比赛中表现的很好，如随机森林。 作为机器学习竞赛世界的新手，我将非常感谢任何改进的建设性指针，感谢您的时间。</p>

</div>
</div>
</div>
    </div>
  </div>
</body>

 


</html>