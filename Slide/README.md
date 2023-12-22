<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"/><title>Weather forecasting with PySpark</title><style>
/* cspell:disable-file */
/* webkit printing magic: print all background colors */
html {
	-webkit-print-color-adjust: exact;
}
* {
	box-sizing: border-box;
	-webkit-print-color-adjust: exact;
}

html,
body {
	margin: 0;
	padding: 0;
}
@media only screen {
	body {
		margin: 2em auto;
		max-width: 900px;
		color: rgb(55, 53, 47);
	}
}

body {
	line-height: 1.5;
	white-space: pre-wrap;
}

a,
a.visited {
	color: inherit;
	text-decoration: underline;
}

.pdf-relative-link-path {
	font-size: 80%;
	color: #444;
}

h1,
h2,
h3 {
	letter-spacing: -0.01em;
	line-height: 1.2;
	font-weight: 600;
	margin-bottom: 0;
}

.page-title {
	font-size: 2.5rem;
	font-weight: 700;
	margin-top: 0;
	margin-bottom: 0.75em;
}

h1 {
	font-size: 1.875rem;
	margin-top: 1.875rem;
}

h2 {
	font-size: 1.5rem;
	margin-top: 1.5rem;
}

h3 {
	font-size: 1.25rem;
	margin-top: 1.25rem;
}

.source {
	border: 1px solid #ddd;
	border-radius: 3px;
	padding: 1.5em;
	word-break: break-all;
}

.callout {
	border-radius: 3px;
	padding: 1rem;
}

figure {
	margin: 1.25em 0;
	page-break-inside: avoid;
}

figcaption {
	opacity: 0.5;
	font-size: 85%;
	margin-top: 0.5em;
}

mark {
	background-color: transparent;
}

.indented {
	padding-left: 1.5em;
}

hr {
	background: transparent;
	display: block;
	width: 100%;
	height: 1px;
	visibility: visible;
	border: none;
	border-bottom: 1px solid rgba(55, 53, 47, 0.09);
}

img {
	max-width: 100%;
}

@media only print {
	img {
		max-height: 100vh;
		object-fit: contain;
	}
}

@page {
	margin: 1in;
}

.collection-content {
	font-size: 0.875rem;
}

.column-list {
	display: flex;
	justify-content: space-between;
}

.column {
	padding: 0 1em;
}

.column:first-child {
	padding-left: 0;
}

.column:last-child {
	padding-right: 0;
}

.table_of_contents-item {
	display: block;
	font-size: 0.875rem;
	line-height: 1.3;
	padding: 0.125rem;
}

.table_of_contents-indent-1 {
	margin-left: 1.5rem;
}

.table_of_contents-indent-2 {
	margin-left: 3rem;
}

.table_of_contents-indent-3 {
	margin-left: 4.5rem;
}

.table_of_contents-link {
	text-decoration: none;
	opacity: 0.7;
	border-bottom: 1px solid rgba(55, 53, 47, 0.18);
}

table,
th,
td {
	border: 1px solid rgba(55, 53, 47, 0.09);
	border-collapse: collapse;
}

table {
	border-left: none;
	border-right: none;
}

th,
td {
	font-weight: normal;
	padding: 0.25em 0.5em;
	line-height: 1.5;
	min-height: 1.5em;
	text-align: left;
}

th {
	color: rgba(55, 53, 47, 0.6);
}

ol,
ul {
	margin: 0;
	margin-block-start: 0.6em;
	margin-block-end: 0.6em;
}

li > ol:first-child,
li > ul:first-child {
	margin-block-start: 0.6em;
}

ul > li {
	list-style: disc;
}

ul.to-do-list {
	padding-inline-start: 0;
}

ul.to-do-list > li {
	list-style: none;
}

.to-do-children-checked {
	text-decoration: line-through;
	opacity: 0.375;
}

ul.toggle > li {
	list-style: none;
}

ul {
	padding-inline-start: 1.7em;
}

ul > li {
	padding-left: 0.1em;
}

ol {
	padding-inline-start: 1.6em;
}

ol > li {
	padding-left: 0.2em;
}

.mono ol {
	padding-inline-start: 2em;
}

.mono ol > li {
	text-indent: -0.4em;
}

.toggle {
	padding-inline-start: 0em;
	list-style-type: none;
}

/* Indent toggle children */
.toggle > li > details {
	padding-left: 1.7em;
}

.toggle > li > details > summary {
	margin-left: -1.1em;
}

.selected-value {
	display: inline-block;
	padding: 0 0.5em;
	background: rgba(206, 205, 202, 0.5);
	border-radius: 3px;
	margin-right: 0.5em;
	margin-top: 0.3em;
	margin-bottom: 0.3em;
	white-space: nowrap;
}

.collection-title {
	display: inline-block;
	margin-right: 1em;
}

.page-description {
    margin-bottom: 2em;
}

.simple-table {
	margin-top: 1em;
	font-size: 0.875rem;
	empty-cells: show;
}
.simple-table td {
	height: 29px;
	min-width: 120px;
}

.simple-table th {
	height: 29px;
	min-width: 120px;
}

.simple-table-header-color {
	background: rgb(247, 246, 243);
	color: black;
}
.simple-table-header {
	font-weight: 500;
}

time {
	opacity: 0.5;
}

.icon {
	display: inline-block;
	max-width: 1.2em;
	max-height: 1.2em;
	text-decoration: none;
	vertical-align: text-bottom;
	margin-right: 0.5em;
}

img.icon {
	border-radius: 3px;
}

.user-icon {
	width: 1.5em;
	height: 1.5em;
	border-radius: 100%;
	margin-right: 0.5rem;
}

.user-icon-inner {
	font-size: 0.8em;
}

.text-icon {
	border: 1px solid #000;
	text-align: center;
}

.page-cover-image {
	display: block;
	object-fit: cover;
	width: 100%;
	max-height: 30vh;
}

.page-header-icon {
	font-size: 3rem;
	margin-bottom: 1rem;
}

.page-header-icon-with-cover {
	margin-top: -0.72em;
	margin-left: 0.07em;
}

.page-header-icon img {
	border-radius: 3px;
}

.link-to-page {
	margin: 1em 0;
	padding: 0;
	border: none;
	font-weight: 500;
}

p > .user {
	opacity: 0.5;
}

td > .user,
td > time {
	white-space: nowrap;
}

input[type="checkbox"] {
	transform: scale(1.5);
	margin-right: 0.6em;
	vertical-align: middle;
}

p {
	margin-top: 0.5em;
	margin-bottom: 0.5em;
}

.image {
	border: none;
	margin: 1.5em 0;
	padding: 0;
	border-radius: 0;
	text-align: center;
}

.code,
code {
	background: rgba(135, 131, 120, 0.15);
	border-radius: 3px;
	padding: 0.2em 0.4em;
	border-radius: 3px;
	font-size: 85%;
	tab-size: 2;
}

code {
	color: #eb5757;
}

.code {
	padding: 1.5em 1em;
}

.code-wrap {
	white-space: pre-wrap;
	word-break: break-all;
}

.code > code {
	background: none;
	padding: 0;
	font-size: 100%;
	color: inherit;
}

blockquote {
	font-size: 1.25em;
	margin: 1em 0;
	padding-left: 1em;
	border-left: 3px solid rgb(55, 53, 47);
}

.bookmark {
	text-decoration: none;
	max-height: 8em;
	padding: 0;
	display: flex;
	width: 100%;
	align-items: stretch;
}

.bookmark-title {
	font-size: 0.85em;
	overflow: hidden;
	text-overflow: ellipsis;
	height: 1.75em;
	white-space: nowrap;
}

.bookmark-text {
	display: flex;
	flex-direction: column;
}

.bookmark-info {
	flex: 4 1 180px;
	padding: 12px 14px 14px;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}

.bookmark-image {
	width: 33%;
	flex: 1 1 180px;
	display: block;
	position: relative;
	object-fit: cover;
	border-radius: 1px;
}

.bookmark-description {
	color: rgba(55, 53, 47, 0.6);
	font-size: 0.75em;
	overflow: hidden;
	max-height: 4.5em;
	word-break: break-word;
}

.bookmark-href {
	font-size: 0.75em;
	margin-top: 0.25em;
}

.sans { font-family: ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol"; }
.code { font-family: "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace; }
.serif { font-family: Lyon-Text, Georgia, ui-serif, serif; }
.mono { font-family: iawriter-mono, Nitti, Menlo, Courier, monospace; }
.pdf .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK JP'; }
.pdf:lang(zh-CN) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK SC'; }
.pdf:lang(zh-TW) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK TC'; }
.pdf:lang(ko-KR) .sans { font-family: Inter, ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol", 'Twemoji', 'Noto Color Emoji', 'Noto Sans CJK KR'; }
.pdf .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK JP'; }
.pdf:lang(zh-CN) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK SC'; }
.pdf:lang(zh-TW) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK TC'; }
.pdf:lang(ko-KR) .code { font-family: Source Code Pro, "SFMono-Regular", Menlo, Consolas, "PT Mono", "Liberation Mono", Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK KR'; }
.pdf .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK JP'; }
.pdf:lang(zh-CN) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK SC'; }
.pdf:lang(zh-TW) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK TC'; }
.pdf:lang(ko-KR) .serif { font-family: PT Serif, Lyon-Text, Georgia, ui-serif, serif, 'Twemoji', 'Noto Color Emoji', 'Noto Serif CJK KR'; }
.pdf .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK JP'; }
.pdf:lang(zh-CN) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK SC'; }
.pdf:lang(zh-TW) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK TC'; }
.pdf:lang(ko-KR) .mono { font-family: PT Mono, iawriter-mono, Nitti, Menlo, Courier, monospace, 'Twemoji', 'Noto Color Emoji', 'Noto Sans Mono CJK KR'; }
.highlight-default {
	color: rgba(55, 53, 47, 1);
}
.highlight-gray {
	color: rgba(120, 119, 116, 1);
	fill: rgba(120, 119, 116, 1);
}
.highlight-brown {
	color: rgba(159, 107, 83, 1);
	fill: rgba(159, 107, 83, 1);
}
.highlight-orange {
	color: rgba(217, 115, 13, 1);
	fill: rgba(217, 115, 13, 1);
}
.highlight-yellow {
	color: rgba(203, 145, 47, 1);
	fill: rgba(203, 145, 47, 1);
}
.highlight-teal {
	color: rgba(68, 131, 97, 1);
	fill: rgba(68, 131, 97, 1);
}
.highlight-blue {
	color: rgba(51, 126, 169, 1);
	fill: rgba(51, 126, 169, 1);
}
.highlight-purple {
	color: rgba(144, 101, 176, 1);
	fill: rgba(144, 101, 176, 1);
}
.highlight-pink {
	color: rgba(193, 76, 138, 1);
	fill: rgba(193, 76, 138, 1);
}
.highlight-red {
	color: rgba(212, 76, 71, 1);
	fill: rgba(212, 76, 71, 1);
}
.highlight-gray_background {
	background: rgba(241, 241, 239, 1);
}
.highlight-brown_background {
	background: rgba(244, 238, 238, 1);
}
.highlight-orange_background {
	background: rgba(251, 236, 221, 1);
}
.highlight-yellow_background {
	background: rgba(251, 243, 219, 1);
}
.highlight-teal_background {
	background: rgba(237, 243, 236, 1);
}
.highlight-blue_background {
	background: rgba(231, 243, 248, 1);
}
.highlight-purple_background {
	background: rgba(244, 240, 247, 0.8);
}
.highlight-pink_background {
	background: rgba(249, 238, 243, 0.8);
}
.highlight-red_background {
	background: rgba(253, 235, 236, 1);
}
.block-color-default {
	color: inherit;
	fill: inherit;
}
.block-color-gray {
	color: rgba(120, 119, 116, 1);
	fill: rgba(120, 119, 116, 1);
}
.block-color-brown {
	color: rgba(159, 107, 83, 1);
	fill: rgba(159, 107, 83, 1);
}
.block-color-orange {
	color: rgba(217, 115, 13, 1);
	fill: rgba(217, 115, 13, 1);
}
.block-color-yellow {
	color: rgba(203, 145, 47, 1);
	fill: rgba(203, 145, 47, 1);
}
.block-color-teal {
	color: rgba(68, 131, 97, 1);
	fill: rgba(68, 131, 97, 1);
}
.block-color-blue {
	color: rgba(51, 126, 169, 1);
	fill: rgba(51, 126, 169, 1);
}
.block-color-purple {
	color: rgba(144, 101, 176, 1);
	fill: rgba(144, 101, 176, 1);
}
.block-color-pink {
	color: rgba(193, 76, 138, 1);
	fill: rgba(193, 76, 138, 1);
}
.block-color-red {
	color: rgba(212, 76, 71, 1);
	fill: rgba(212, 76, 71, 1);
}
.block-color-gray_background {
	background: rgba(241, 241, 239, 1);
}
.block-color-brown_background {
	background: rgba(244, 238, 238, 1);
}
.block-color-orange_background {
	background: rgba(251, 236, 221, 1);
}
.block-color-yellow_background {
	background: rgba(251, 243, 219, 1);
}
.block-color-teal_background {
	background: rgba(237, 243, 236, 1);
}
.block-color-blue_background {
	background: rgba(231, 243, 248, 1);
}
.block-color-purple_background {
	background: rgba(244, 240, 247, 0.8);
}
.block-color-pink_background {
	background: rgba(249, 238, 243, 0.8);
}
.block-color-red_background {
	background: rgba(253, 235, 236, 1);
}
.select-value-color-uiBlue { background-color: rgba(35, 131, 226, .07); }
.select-value-color-pink { background-color: rgba(245, 224, 233, 1); }
.select-value-color-purple { background-color: rgba(232, 222, 238, 1); }
.select-value-color-green { background-color: rgba(219, 237, 219, 1); }
.select-value-color-gray { background-color: rgba(227, 226, 224, 1); }
.select-value-color-translucentGray { background-color: rgba(255, 255, 255, 0.0375); }
.select-value-color-orange { background-color: rgba(250, 222, 201, 1); }
.select-value-color-brown { background-color: rgba(238, 224, 218, 1); }
.select-value-color-red { background-color: rgba(255, 226, 221, 1); }
.select-value-color-yellow { background-color: rgba(253, 236, 200, 1); }
.select-value-color-blue { background-color: rgba(211, 229, 239, 1); }
.select-value-color-pageGlass { background-color: undefined; }
.select-value-color-washGlass { background-color: undefined; }

.checkbox {
	display: inline-flex;
	vertical-align: text-bottom;
	width: 16;
	height: 16;
	background-size: 16px;
	margin-left: 2px;
	margin-right: 5px;
}

.checkbox-on {
	background-image: url("data:image/svg+xml;charset=UTF-8,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20viewBox%3D%220%200%2016%2016%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%0A%3Crect%20width%3D%2216%22%20height%3D%2216%22%20fill%3D%22%2358A9D7%22%2F%3E%0A%3Cpath%20d%3D%22M6.71429%2012.2852L14%204.9995L12.7143%203.71436L6.71429%209.71378L3.28571%206.2831L2%207.57092L6.71429%2012.2852Z%22%20fill%3D%22white%22%2F%3E%0A%3C%2Fsvg%3E");
}

.checkbox-off {
	background-image: url("data:image/svg+xml;charset=UTF-8,%3Csvg%20width%3D%2216%22%20height%3D%2216%22%20viewBox%3D%220%200%2016%2016%22%20fill%3D%22none%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%3E%0A%3Crect%20x%3D%220.75%22%20y%3D%220.75%22%20width%3D%2214.5%22%20height%3D%2214.5%22%20fill%3D%22white%22%20stroke%3D%22%2336352F%22%20stroke-width%3D%221.5%22%2F%3E%0A%3C%2Fsvg%3E");
}
	
</style></head><body><article id="c6df8301-ae40-4b81-9a26-242936f0c6fc" class="page sans"><header><h1 class="page-title"><strong><strong>Weather forecasting with PySpark</strong></strong></h1><p class="page-description"></p></header><div class="page-body"><p id="5f19a176-ffee-4282-9738-0c5e449202a1" class="">Github Repository</p><figure id="d3cf7742-d29f-43f3-a4fc-4bd8ef901eff"><div class="source">https://github.com/ngaymai/Big-data-for-weather-forecasting</div></figure><details open=""><summary style="font-weight:600;font-size:1.875em;line-height:1.3;margin:0">1. <strong>Introduction</strong></summary><div class="indented"><details open=""><summary style="font-weight:600;font-size:1.5em;line-height:1.3;margin:0"><strong>Problem Statement:</strong></summary><div class="indented"><p id="55e6d0bc-c452-4f7c-870a-2c7e5ca27921" class="">Weather forecasting, the science of predicting atmospheric conditions, has always been a challenging task due to the complex and dynamic nature of the Earth’s atmosphere. The atmosphere is a chaotic system, influenced by a multitude of factors ranging from large-scale weather patterns to local geographical features. This makes weather forecasting an inherently difficult problem. Despite the difficulty, accurate weather prediction is crucial for a variety of applications, ranging from agricultural planning to disaster management. Traditional methods of weather forecasting involve physical models of the atmosphere, which require significant computational resources and are not always accurate.</p></div></details><details open=""><summary style="font-weight:600;font-size:1.5em;line-height:1.3;margin:0"><strong>Applications:</strong></summary><div class="indented"><p id="70e2481a-96c9-4faf-9204-bad17208903f" class="">The importance of weather forecasting cannot be overstated, given its wide-ranging applications in various fields. In agriculture, accurate weather predictions can help farmers plan their sowing and harvesting activities, thereby maximizing crop yield and minimizing losses due to adverse weather conditions. In aviation, accurate weather forecasts can enable airlines to plan their routes more efficiently, ensuring passenger safety and saving fuel costs. In the field of defense, accurate weather predictions can assist defense forces in strategic planning, providing them with a tactical advantage. For tourists, accurate weather forecasts can help them plan their travels, ensuring they can make the most of their vacations. Lastly, in the case of severe weather conditions, accurate and timely weather forecasts can aid in timely evacuation, potentially saving lives.</p><p id="6f53d389-0fd2-4895-8b34-3e2b5e121e7d" class="">
</p></div></details><details open=""><summary style="font-weight:600;font-size:1.5em;line-height:1.3;margin:0"><strong>Existing Solutions and Their Limitations:</strong></summary><div class="indented"><p id="e89449ee-7105-49c7-9609-368f2fae65ce" class="">The traditional methods of weather forecasting, such as persistence and trend methods, statistical methods, and numerical weather prediction (NWP), each have their own set of advantages and disadvantages. Persistence and trend methods are simple to use but may not be accurate for longer periods. These methods assume that the weather conditions will remain the same (persistence) or follow the same trend (trend) as observed in the recent past. While these methods can provide reasonably accurate forecasts for short periods, their accuracy diminishes for longer periods.</p><p id="be5177db-a15d-4cbf-bd07-b05e41d79fa4" class="">
</p><p id="4956c3bf-0330-4b90-8fa0-28361e61521d" class="">Statistical methods, while being more accurate than persistence and trend methods, require extensive historical data. These methods use statistical techniques to find relationships between current weather patterns and past weather data. However, the accuracy of these methods is dependent on the availability and quality of historical data.</p><p id="d554e3b1-669a-4ddb-a3c2-981aeb48c082" class="">
</p><p id="3de178f0-99d3-4c0a-91e0-9f7a369df9ba" class="">NWP, on the other hand, provides the most accurate forecasts but requires significant computational resources and expertise. NWP involves simulating the atmosphere using complex mathematical models. While these models can capture the dynamics of the atmosphere more accurately, they are computationally intensive and require a deep understanding of atmospheric physics.</p><p id="da48de46-1117-4edf-9ef7-8b7c2467104b" class="">
</p></div></details><details open=""><summary style="font-weight:600;font-size:1.5em;line-height:1.3;margin:0"><strong>Our Approach:</strong> </summary><div class="indented"><p id="bb2f4c15-3d0d-4240-a911-1c752b22a955" class="">Given the limitations of the existing methods, we choose to explore the use of Machine Learning (ML) for weather forecasting. ML models, with their ability to learn complex patterns from data, provide a promising alternative to traditional methods. In this project, we use PySpark, a Python library for big data processing, to implement and evaluate various ML models such as logistic regression, SVM, and random forest for weather forecasting. Our choice of PySpark is motivated by its ability to handle large datasets and perform distributed computing, making it suitable for big data applications. By leveraging the power of ML and big data, we aim to develop a weather forecasting model that is both accurate and scalable.</p><p id="205c0f9f-504f-45a6-85ef-dd1bbae230d6" class="">
</p></div></details></div></details><details open=""><summary style="font-weight:600;font-size:1.875em;line-height:1.3;margin:0">2. <strong>Methods/Approaches</strong></summary><div class="indented"><p id="7974c99b-240f-4274-a83d-d5537525f903" class=""><strong>Overview:</strong> In this project, we utilize PySpark, a Python library for big data processing, to implement and evaluate various machine learning models such as logistic regression, SVM, and random forest for weather forecasting. We chose PySpark due to its ability to handle large datasets and perform distributed computing, making it suitable for big data applications.</p><p id="4cd57821-0c42-4cf2-9703-507ff29a43a2" class=""><strong>Architecture/Method Pipeline:</strong> Our process consists of three main steps: data preprocessing, model training, and weather prediction.</p><ol type="1" id="9506886d-b090-4c39-be8f-f17257fed1e9" class="numbered-list" start="1"><li><strong>Data Preprocessing:</strong> Initially, we preprocess the dataset to prepare it for the machine learning process. This step includes handling missing data, removing noise, and normalizing the data. We also convert the weather data into a numerical form to suit the machine learning models.</li></ol><ol type="1" id="16d035fe-91fa-42bc-8057-50debc7d8a3b" class="numbered-list" start="2"><li><strong>Model Training:</strong> After preprocessing, we split the dataset into two parts: one for training the model and one for testing the model’s accuracy. We then train various machine learning models such as logistic regression, SVM, and random forest on the training dataset.</li></ol><ol type="1" id="1628d842-4f4f-4775-9e94-116c74c9a13e" class="numbered-list" start="3"><li><strong>Weather Prediction:</strong> Finally, we use the trained models to predict weather conditions based on current weather data. We then evaluate the accuracy of the predictions by comparing them with actual data.</li></ol><p id="1d804bc2-eca5-4f2e-b82a-c43505c3d43c" class=""><strong>Main Steps:</strong> The main steps in our process include:</p><ol type="1" id="83b1c85d-e6f6-4738-8612-35bf62c59487" class="numbered-list" start="1"><li><strong>Data Preprocessing:</strong> We preprocess the data to remove noise and normalize the data, preparing it for the machine learning process.</li></ol><ol type="1" id="2095a01c-a844-4014-8248-29316983bc9a" class="numbered-list" start="2"><li><strong>Model Training:</strong> We train various machine learning models such as logistic regression, SVM, and random forest on the preprocessed dataset.</li></ol><ol type="1" id="ddbeb809-4481-4a97-8a2a-6e2a1964fd42" class="numbered-list" start="3"><li><strong>Weather Prediction:</strong> We use the trained models to predict weather conditions based on current weather data.</li></ol><ol type="1" id="cab424b6-01e1-4fbf-909e-a50b2500b9a3" class="numbered-list" start="4"><li><strong>Model Evaluation:</strong> We evaluate the accuracy of the predictions by comparing them with actual data. We also evaluate the performance of the models to determine which model works best for our project.</li></ol></div></details><details open=""><summary style="font-weight:600;font-size:1.875em;line-height:1.3;margin:0">3. Experiments</summary><div class="indented"><p id="85d9e795-ab51-449e-83f3-3c50d394ffe2" class="">
</p><p id="1f0c21d4-1539-4335-af77-fd11e32b6413" class=""><strong>Overview:</strong> In this project, we utilize PySpark, a Python library for big data processing, to implement and evaluate various machine learning models such as logistic regression, SVM, and random forest for weather forecasting. We chose PySpark due to its ability to handle large datasets and perform distributed computing, making it suitable for big data applications.</p><p id="c1114177-4cc5-4269-ba91-ac959b4597b5" class="">
</p><p id="f26738d1-aed1-46cd-b1c1-2d3818cbfcaa" class="">
</p><details open=""><summary style="font-weight:600;font-size:1.25em;line-height:1.3;margin:0">3.1 Desciption</summary><div class="indented"><p id="b0225f05-a68f-4605-a750-b4bfd475434d" class=""><strong>Implementation description</strong>: The project uses <strong>PySpark</strong> and <strong>MLlib</strong> to implement a <strong>distributed machine learning pipeline</strong> for weather forecasting. The pipeline consists of four stages: data ingestion, data preprocessing, model training, and model evaluation. The code for the pipeline is written in a <strong>Jupyter notebook</strong> and can be run on a <strong>Databricks</strong> environment.</p><p id="5cb7238d-f6bd-48dd-a742-7f6bc689e57b" class="">
</p><p id="1e1463ac-8855-4d57-8d9d-cf5511480205" class=""><strong>Testing for benchmark datasets</strong>: The project benchmark datasets from <a href="https://www.kaggle.com/datasets/selfishgene/historical-hourly-weather-data">https://www.kaggle.com/datasets/selfishgene/historical-hourly-weather-data</a> for testing the pipeline:</p><p id="1452c632-943a-4e53-ad26-d74fb593b7c6" class="">
</p><p id="5f994385-0207-45c0-8718-08a40db9cf50" class="">The dataset is a collection of hourly weather data for 30 US and Canadian cities and 6 Israeli cities from 2012 to 2017. The dataset contains the following files:</p><p id="bc3ebd15-9b57-4aa9-9dc9-a4bfa93ae03f" class=""><div class="indented"><ul id="832cb4af-4e49-4904-9704-6ba03cfc1131" class="bulleted-list"><li style="list-style-type:disc"><code>temperature.csv</code>: Hourly temperature data in Kelvin.</li></ul><ul id="22e5f2d1-4462-43d0-91b1-7f1dfca86225" class="bulleted-list"><li style="list-style-type:disc"><code>humidity.csv</code>: Hourly humidity data in percentage.</li></ul><ul id="1b61cf32-f928-446a-8ddd-c8d919ad9afe" class="bulleted-list"><li style="list-style-type:disc"><code>pressure.csv</code>: Hourly atmospheric pressure data in millibars.</li></ul><ul id="f35fb812-bcb6-4de7-a969-338b402ba0c0" class="bulleted-list"><li style="list-style-type:disc"><code>wind_direction.csv</code>: Hourly wind direction data in degrees.</li></ul><ul id="1efa094e-9222-40ee-92c3-e94490e84ad3" class="bulleted-list"><li style="list-style-type:disc"><code>wind_speed.csv</code>: Hourly wind speed data in meters per second.</li></ul><ul id="41a2da05-f119-4ef1-b166-392c67c3369a" class="bulleted-list"><li style="list-style-type:disc"><code>weather_description.csv</code>: Hourly textual description of the weather.</li></ul><ul id="453bfd9d-cce7-4dea-b7d4-c28fd17bf86d" class="bulleted-list"><li style="list-style-type:disc"><code>city_attributes.csv</code>: Information about the cities, such as name, country, latitude, and longitude.</li></ul><p id="453107ff-e689-4a1a-8648-bfcc249c1ad9" class="">
</p></div></p><p id="c886d3af-1f86-42f3-b2eb-e765c5f98db2" class="">The dataset can be used for various data analysis and visualization tasks, such as exploring the correlations between different weather variables, comparing the weather patterns across different cities, or predicting the weather based on historical data.</p></div></details><p id="7a685f57-37bf-43be-985e-4eaa52cdbe82" class="">
</p><details open=""><summary style="font-weight:600;font-size:1.25em;line-height:1.3;margin:0">3.2 <strong><strong>Data Preprocessing</strong></strong></summary><div class="indented"><p id="22518d65-a4d7-4a3e-9b15-50d9a946dea3" class="">
</p><figure class="block-color-gray_background callout" style="white-space:pre-wrap;display:flex" id="ad0b0f78-64a9-40f4-8d09-7623d19b7361"><div style="font-size:1.5em"><span class="icon">💡</span></div><div style="width:100%"><strong>Download the dataset</strong><p id="4ae20fde-8538-499b-b9b0-d48212b82dda" class="">Original source: <a href="https://www.kaggle.com/selfishgene/historical-hourly-weather-data">kaggle.com/selfishgene/historical-hourly-weather-data</a></p></div></figure><p id="ca0303bc-8d16-41d0-a650-94027529679c" class="">
</p><p id="18ad99bb-30dd-4464-b46a-6aa932f43838" class="">We will get the .zip file and we must to extract all to get 7 .csv files</p><p id="59929d33-7e25-4286-9ab0-ba3bbb8a15e7" class="">After that, we load dataset to object</p><p id="8d7fa473-406d-4883-bf3f-7b357859f7ba" class="">
</p><h3 id="6fe010c6-f93f-4505-af19-4696db46f41f" class="">3.2. <strong><strong>Load dataset into Koalas </strong></strong><code><strong><strong>DataFrame</strong></strong></code><strong><strong> objects</strong></strong></h3><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="f2e368ea-fceb-48f8-b3c6-766280b1214e" class="code"><code class="language-Python">weather_conditions_df = ks.read_csv(f&#x27;{DATASET_PATH}weather_description.csv&#x27;)
humidity_df = ks.read_csv(f&#x27;{DATASET_PATH}humidity.csv&#x27;)
pressure_df = ks.read_csv(f&#x27;{DATASET_PATH}pressure.csv&#x27;)
temperature_df = ks.read_csv(f&#x27;{DATASET_PATH}temperature.csv&#x27;)
city_attributes_df = ks.read_csv(f&#x27;{DATASET_PATH}city_attributes.csv&#x27;)
wind_direction_df = ks.read_csv(f&#x27;{DATASET_PATH}wind_direction.csv&#x27;)
wind_speed_df = ks.read_csv(f&#x27;{DATASET_PATH}wind_speed.csv&#x27;)</code></pre><p id="095ae8b1-d7d9-40f6-9383-f15b1f494b24" class="">
</p><p id="dd7aa92b-ab31-4292-a9f7-99add268f51d" class="">To prepare for working, we must to create a new single dataframe with including all collected information for Machine Learning</p><p id="26078f74-b796-4948-8282-ad48eeb1e0f9" class="">
</p><p id="51ae45d2-1b75-45b0-81c9-d7cad73aff07" class=""><strong><strong>Create a single </strong></strong><code><strong><strong>DataFrame</strong></strong></code><strong><strong> that includes all data from the others</strong></strong></p><p id="2ae3a116-bf5d-411c-af30-7f9b6b1471bf" class="">
</p><p id="398ce9e2-0707-42df-896b-23c87e1a58c2" class="">We create a function to filter the city</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="fe80bcba-0e9b-4abd-96f2-eb1f124193af" class="code"><code class="language-Python">def filter_dataframe_by_city_column(dataframe: ks.DataFrame,
                                    city_name: str,
                                    new_column_name: str) -&gt; DataFrame:
    &#x27;&#x27;&#x27;
    Args:
        - dataframe: a `DataFrame` with a datetime column and n cities columns,
                     where the records are the related hourly measurements
        - city_name: city name between the ones in the dataframe
        - new_column_name: name to replace the city name
        
    Returns: 
        a new `DataFrame` with:
            - the datetime column
            - a single column of measurements related to the `city_name`
              and renamed as `new_column_name`
    &#x27;&#x27;&#x27;
    return dataframe.to_spark() \
        .withColumn(new_column_name, col(city_name)) \
        .select([DATETIME_COL, new_column_name])</code></pre><p id="e5c4549a-9cf4-416f-b646-02d23e0f7208" class="">
</p><p id="28ff1c3a-8bd4-499b-9740-52f9d8bdd751" class="">After that, we write a function for data joining</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="51245a47-7379-42a7-8a16-33ec1dfbcbdd" class="code"><code class="language-Python">def join_dataframes(dataframes: List[DataFrame], column_name: str) -&gt; DataFrame:
    &#x27;&#x27;&#x27;
    Args:
        - dataframse: a list of `DataFrame` to be joined
        - column_name: the column over which the records should be joined
        
    Returns:
        a new dataframes resulting from the join of all the dataframes
        over the `column_name` column
    &#x27;&#x27;&#x27;
    joined_df = dataframes[0]

    for dataframe in dataframes[1:]:
        joined_df = joined_df.join(dataframe, [column_name])

    return joined_df</code></pre><p id="3c9d66b8-5035-4b66-bca7-02caaaaf5ea0" class="">
</p><p id="203d6247-f084-4f95-99b4-55fa0ccb557d" class="">And using for loop to create a new dataset:</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="c199fb75-5da8-4be5-8b6b-e6c420ad55f3" class="code"><code class="language-Python">weather_measurements_df = None

# Iterate over all the records in the cities `DataFrame`
for index, row in city_attributes_df.iterrows():    

    city = row.City
    country = row.Country
    latitude = row.Latitude
    longitude = row.Longitude

    # Compute a list of `DataFrame`, one for each type of measurement in the city
    dataframes = [
        filter_dataframe_by_city_column(humidity_df, city, HUMIDITY_COL),
        filter_dataframe_by_city_column(pressure_df, city, PRESSURE_COL),
        filter_dataframe_by_city_column(temperature_df, city, TEMPERATURE_COL),
        filter_dataframe_by_city_column(wind_direction_df, city, WIND_DIRECTION_COL),
        filter_dataframe_by_city_column(wind_speed_df, city, WIND_SPEED_COL),
        filter_dataframe_by_city_column(weather_conditions_df, city, WEATHER_CONDITION_COL)
    ]

    # Compute a `DataFrame` that includes all the data about the measurements in the city
    joined_df = join_dataframes(dataframes, DATETIME_COL) \
        .withColumn(CITY_COL, lit(city)) \
        .withColumn(COUNTRY_COL, lit(country)) \
        .withColumn(LATITUDE_COL, lit(latitude)) \
        .withColumn(LONGITUDE_COL, lit(longitude))

    # Union the `DataFrame` with the ones computed in the previous iterations
    weather_measurements_df = weather_measurements_df.union(joined_df) if weather_measurements_df is not None else joined_df</code></pre><p id="b34b895f-beb0-4107-a7f1-96206f4dc5e9" class="">
</p><p id="5e7cf8d2-e6b0-43a3-855b-2925c55a1d1f" class="">We print the new schema and shape to re-check again and we get</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="9008c25d-e817-4756-bc4b-ad4ea49932eb" class="code"><code class="language-JavaScript">The shape of the dataset is 1629108 rows by 11 columns</code></pre><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="192a3d3a-d32d-4f74-9cea-5016696c1bac" class="code"><code class="language-JavaScript">root
|-- datetime: timestamp (nullable = true)
|-- humidity: double (nullable = true)
|-- pressure: double (nullable = true)
|-- temperature: double (nullable = true)
|-- wind_direction: double (nullable = true)
|-- wind_speed: double (nullable = true)
|-- weather_condition: string (nullable = true)
|-- city: string (nullable = false)
|-- country: string (nullable = false)
|-- latitude: double (nullable = false)
|-- longitude: double (nullable = false)</code></pre></div></details><p id="41a1d05c-aeaf-47a0-864b-ebbd48550f1c" class=""><div class="indented"><p id="81226e92-a9d6-436a-b4f1-f56706fd9f4c" class="">All right, the output as we expected, however, the problem is that the measurements in the dataset can have missing values for some of the metrics.</p><p id="ef73f051-043d-4e9f-8dd1-b874aaa84844" class="">
</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="b1deb6e3-7bfc-4a40-8593-126c016661d6" class="code"><code class="language-Python">if SLOW_OPERATIONS:
    for c in weather_measurements_df.columns:
        print(f&#x27;Missing values of column `{c}` count: {weather_measurements_df.where(col(c).isNull()).count()}&#x27;)</code></pre><p id="5dd0baad-1a7c-4790-917d-bdf0d6914645" class="">
</p><p id="3b676c6e-08f3-4302-85d4-763403929efa" class="">We get:</p><figure class="block-color-gray_background callout" style="white-space:pre-wrap;display:flex" id="f4c45d54-b4e9-4c42-b24d-cf1bfb9825cf"><div style="font-size:1.5em"><span class="icon">💡</span></div><div style="width:100%">Missing values of column <code>datetime</code> count: 0<br/>Missing values of column <br/><code>humidity</code> count: 28651<br/>Missing values of column <br/><code>pressure</code> count: 16680<br/>Missing values of column <br/><code>temperature</code> count: 8030<br/>Missing values of column <br/><code>wind_direction</code> count: 7975<br/>Missing values of column <br/><code>wind_speed</code> count: 7993<br/>Missing values of column <br/><code>weather_condition</code> count: 8083<br/>Missing values of column <br/><code>city</code><code>country</code><code>latitude</code><code>longitude</code> count: 0</div></figure><p id="a31189a1-bf57-4b8e-8176-c3fd707ecd8c" class="">
</p><p id="0989b027-e280-4d3d-9dbb-746ed571c635" class="">To address this issue, there are two possible approaches:<div class="indented"><ol type="1" id="5a13557e-a985-4c1c-aa7d-022d67152535" class="numbered-list" start="1"><li><mark class="highlight-blue"><code><strong>Remove all rows</strong></code></mark> that have null values.</li></ol><ol type="1" id="29c7f39e-14ed-41c5-8b1c-614d85ad18f0" class="numbered-list" start="2"><li><mark class="highlight-blue"><code><strong>Replace null values</strong></code></mark> with representative ones, such as their mean.</li></ol></div></p><p id="728cc7d6-7376-4ec2-9d18-e6ca53a17b75" class="">
</p><p id="b47566e2-7ed9-4612-b3fd-56fb2dbf576f" class="">Considering the s<strong>ubstantial amount of data available</strong>, it is advisable to <strong>drop the null rows.</strong> This will ensure that we still have a sufficient amount of data to train a Machine Learning model effectively. Additionally, keeping only actual measurements in the dataset will prevent any potential inaccurate predictions caused by artificial values.</p><p id="66ee068d-673b-4c8c-a1c0-8db376475792" class="">
</p><p id="691e33d9-df4c-4b30-8d88-afee43b35274" class=""><strong><strong>Clean the dataset from measurements with missing metrics</strong></strong></p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="4e16e630-bfb2-4958-8507-18a796d504a3" class="code"><code class="language-Python">not_null_weather_measurements_df = weather_measurements_df.dropna()</code></pre><p id="9a95dfea-f3a3-4126-9721-e5fbe8070b16" class="">
</p><p id="546fdd9e-5e42-4260-873b-ff15fa0dd453" class="">
</p></div></p><details open=""><summary style="font-weight:600;font-size:1.25em;line-height:1.3;margin:0">3.2.2 <strong><strong>Aggregation</strong></strong></summary><div class="indented"><p id="08769a59-98a1-4c29-8c32-7b6513434900" class="">
</p><p id="0b870d6d-34ff-4e0a-85a2-5008f0c6f7cd" class="">The target classes for our weather forecasting classification task appear to be quite sparse in the original dataset. Within the dataset, we have <mark class="highlight-orange"><code><strong>54 distinct weather conditions</strong></code></mark>, but it is worth noting that some of these conditions occur very infrequently while many of them are quite similar to each other.</p><p id="cd5c503c-21c0-41b3-be92-48759642afce" class=""><br/>For instance, if we consider the conditions related to thunderstorms, we find that the following conditions essentially convey the same meteorological situation:<br/></p><ol type="1" id="b05be55d-a60a-450e-a204-4591a1162587" class="numbered-list" start="1"><li>Thunderstorm with light drizzle.</li></ol><ol type="1" id="6f8c99cc-0a2f-4dd1-b722-ba9fc0bbe7f9" class="numbered-list" start="2"><li>Thunderstorm with rain.</li></ol><ol type="1" id="65986f06-75c9-4cf1-ba47-642888ba9efc" class="numbered-list" start="3"><li>Thunderstorm with light rain.</li></ol><p id="f53aad5f-e673-4849-8efe-5066d589de5b" class=""><br/>Given the similarity between these conditions, it becomes advantageous to categorize them as a single meteorological condition. In order to enhance the quality of our target classes, it is necessary to preprocess the dataset and aggregate some of these similar weather conditions. By doing so, we will obtain a more refined and representative set of target classes.<br/></p><p id="cdc9b7fd-34bf-4b9e-abbf-6f47af5cdf33" class="">
</p><p id="426073d1-bfef-4232-aff8-39385ed8daf0" class=""><strong>Count and display the number of data samples for each type of weather condition in the DataFrame.</strong></p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="b961b2af-d6c5-4616-b259-03facbf7a88c" class="code"><code class="language-Python">if SLOW_OPERATIONS: not_null_weather_measurements_df.groupBy
   (WEATHER_CONDITION_COL).count().show(truncate=False)</code></pre><p id="72fbf948-d90e-4f1c-a063-8e0addbe8690" class=""><strong>The result: </strong></p><table id="4d42c237-7be3-4d9e-9360-28def2c8eeb2" class="simple-table"><tbody><tr id="b29b63ac-3de6-4a83-8a56-26cc4d991f09"><td id=";hmO" class="" style="width:366.2604217529297px">Weather Condition</td><td id="nviZ" class="">Count</td></tr><tr id="82101381-7a3f-4f97-a9b0-d16955b29111"><td id=";hmO" class="" style="width:366.2604217529297px">fog</td><td id="nviZ" class="">16185</td></tr><tr id="eca055ca-435a-4508-b69c-57533481d7b3"><td id=";hmO" class="" style="width:366.2604217529297px">very heavy rain</td><td id="nviZ" class="">1001</td></tr><tr id="3e050efd-059c-4235-92c2-af53d35ae9bd"><td id=";hmO" class="" style="width:366.2604217529297px">proximity shower rain</td><td id="nviZ" class="">2339</td></tr><tr id="d5bf4939-e342-4dfe-b47f-cec825c79ca3"><td id=";hmO" class="" style="width:366.2604217529297px">few clouds</td><td id="nviZ" class="">133685</td></tr><tr id="6fbc4b04-7a8b-42af-b8d7-886d2a49f95f"><td id=";hmO" class="" style="width:366.2604217529297px">heavy shower snow</td><td id="nviZ" class="">336</td></tr><tr id="bac4aebe-eba3-47da-936f-a18ae8cfc5c4"><td id=";hmO" class="" style="width:366.2604217529297px">light rain</td><td id="nviZ" class="">127364</td></tr><tr id="254a74d7-24e2-4c74-aff8-0f922fcb69cb"><td id=";hmO" class="" style="width:366.2604217529297px">light intensity drizzle</td><td id="nviZ" class="">8048</td></tr><tr id="d4e78bae-abdd-4454-99f4-42cf084f59f8"><td id=";hmO" class="" style="width:366.2604217529297px">light intensity shower rain</td><td id="nviZ" class="">3633</td></tr><tr id="179f9b4a-ece8-4845-adb0-85cc10fcbc8c"><td id=";hmO" class="" style="width:366.2604217529297px">broken clouds</td><td id="nviZ" class="">167102</td></tr><tr id="22b8b4b3-596c-4dd2-b29b-567a79af426c"><td id=";hmO" class="" style="width:366.2604217529297px">overcast clouds</td><td id="nviZ" class="">133778</td></tr><tr id="fabe1a72-a8d2-417f-a993-5a579e40a2aa"><td id=";hmO" class="" style="width:366.2604217529297px">light snow</td><td id="nviZ" class="">14368</td></tr><tr id="bc14d6b0-524a-406f-8741-98e1c75fc684"><td id=";hmO" class="" style="width:366.2604217529297px">scattered clouds</td><td id="nviZ" class="">143277</td></tr><tr id="b7b88965-cba6-4269-8b66-b0144449a3ec"><td id=";hmO" class="" style="width:366.2604217529297px">thunderstorm with heavy rain</td><td id="nviZ" class="">396</td></tr><tr id="ea2305bc-6fcb-4b21-adee-4df80f8f39a5"><td id=";hmO" class="" style="width:366.2604217529297px">thunderstorm with light rain</td><td id="nviZ" class="">1179</td></tr><tr id="605230e4-48ac-4db7-9a39-79ce9c92b6b8"><td id=";hmO" class="" style="width:366.2604217529297px">heavy intensity rain</td><td id="nviZ" class="">14075</td></tr><tr id="a15bcac6-4532-472e-bbb9-45bb3df6880a"><td id=";hmO" class="" style="width:366.2604217529297px">moderate rain</td><td id="nviZ" class="">43172</td></tr><tr id="c51381f3-432d-4966-9851-e8b1367749c0"><td id=";hmO" class="" style="width:366.2604217529297px">light intensity drizzle rain</td><td id="nviZ" class="">41</td></tr><tr id="bd281286-dbdf-423f-bd2f-0af1c6e15217"><td id=";hmO" class="" style="width:366.2604217529297px">sky is clear</td><td id="nviZ" class="">641577</td></tr><tr id="b64c4b9d-acef-483a-a62e-c2e80d642095"><td id=";hmO" class="" style="width:366.2604217529297px">snow</td><td id="nviZ" class="">3156</td></tr><tr id="903a423f-09ae-40b9-ad3a-9b516ce94797"><td id=";hmO" class="" style="width:366.2604217529297px">light shower snow</td><td id="nviZ" class="">998</td></tr></tbody></table><p id="b2110526-cc6e-4594-8c0c-ff78acd6bb5c" class="">
</p><p id="8fee8ba0-832b-447a-9303-de2a621c962d" class="">To clear, see the sorted chart below: </p><p id="6cdca24b-d99b-4599-9a31-4247537c9d79" class="">
</p><figure id="85568e74-b071-47b3-8997-b9c34fb1b32c" class="image"><a href="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled.png"><img style="width:2310px" src="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled.png"/></a></figure><p id="cfd0825f-3c23-417c-a479-252574ff36de" class="">
</p><p id="d6bb7fc9-5a78-4a53-a2a2-dbd6b4f9d3fe" class="">To enhance the quality of target classes, we will <strong>condenser the original 54 classes into 6 aggregated categories</strong>.</p><p id="6f3fe72b-2df4-4679-9dae-7b8d75acaeaa" class="">
</p><table id="bb7ebc01-d251-4745-968f-8506c3a2d219" class="simple-table"><tbody><tr id="82dade38-ad3b-4ac9-87e0-e47cc129f014"><td id="az[|" class="" style="width:213px">• thunderstorm</td><td id="{Jzb" class="" style="width:218px">• rainy</td><td id="aHvr" class="" style="width:165px">• snowy</td></tr><tr id="e47d406a-5833-4c76-968a-b9a19ae5b70f"><td id="az[|" class="" style="width:213px">• cloudy</td><td id="{Jzb" class="" style="width:218px">• foggy</td><td id="aHvr" class="" style="width:165px">• sunny</td></tr></tbody></table><p id="3831fe24-baf4-4f70-b5c8-855b55f84b5c" class="">
</p><p id="ef7960fe-34aa-4d05-a86b-64b3d439c9cc" class=""><mark class="highlight-blue"><strong><code>Function:</code></strong></mark></p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="b7fc5581-4a2a-48c6-8cec-f2a0d7ea65dd" class="code"><code class="language-Python">def get_weather_conditions_aggregation_dict(weather_conditions: Iterable[str]) -&gt; Dict[str, str]:
    &#x27;&#x27;&#x27;
    Args:
        - weather_conditions: an iterable collection of string weather conditions to be aggregated

    Returns:
        a dictionary that goes from the original weather condition name to one among the following:
            - thunderstorm
            - rainy
            - snowy
            - cloudy
            - foggy
            - sunny
    &#x27;&#x27;&#x27;
    
    weather_conditions_dict = dict()
  
    for weather_condition in weather_conditions:
  
        weather_condition_lowered = weather_condition.lower()

        if any(key in weather_condition_lowered for key in [&#x27;squall&#x27;, &#x27;thunderstorm&#x27;]):
            weather_conditions_dict[weather_condition] = &#x27;thunderstorm&#x27;
        elif any(key in weather_condition_lowered for key in [&#x27;drizzle&#x27;, &#x27;rain&#x27;]):
            weather_conditions_dict[weather_condition] = &#x27;rainy&#x27;
        elif any(key in weather_condition_lowered for key in [&#x27;sleet&#x27;, &#x27;snow&#x27;]):
            weather_conditions_dict[weather_condition] = &#x27;snowy&#x27;
        elif &#x27;cloud&#x27; in weather_condition_lowered:
            weather_conditions_dict[weather_condition] = &#x27;cloudy&#x27;
        elif any(key in weather_condition_lowered for key in [&#x27;fog&#x27;, &#x27;mist&#x27;, &#x27;haze&#x27;]):
            weather_conditions_dict[weather_condition] = &#x27;foggy&#x27;
        elif any(key in weather_condition_lowered for key in [&#x27;clear&#x27;, &#x27;sun&#x27;]):
            weather_conditions_dict[weather_condition] = &#x27;sunny&#x27;
            
    return weather_conditions_dict</code></pre><p id="5bbafb3a-ee34-4ec7-87ea-fd2f868e2401" class="">and: </p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="ad6b4520-7b13-4d3a-8fbe-5d715cc6a5a7" class="code"><code class="language-Python">weather_conditions_all = not_null_weather_measurements_df \
    .select(WEATHER_CONDITION_COL).distinct() \
    .to_koalas().to_numpy().reshape(-1)</code></pre><p id="6e98b300-8fd2-4527-9b99-900e5c153103" class="">create new data:</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="0ecd44f9-4584-497a-9a50-abee7346c9d5" class="code"><code class="language-Python">weather_conditions_dict = get_weather_conditions_aggregation_dict(weather_conditions_all)</code></pre><p id="65003748-741f-4c2e-8381-970d3cdbba52" class="">
</p><p id="c0d19974-96d7-4ab0-9c09-d0a5bd7b0681" class=""><strong><strong>Replace all the weather conditions in the </strong></strong><code><strong><strong>DataFrame</strong></strong></code><strong><strong> with the aggregated ones</strong></strong></p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="29dce929-3385-4fbf-b7d2-b3fc85ee27d9" class="code"><code class="language-Python">weather_measurements_aggregated_df = not_null_weather_measurements_df.replace(weather_conditions_dict)</code></pre><p id="b3286c77-454b-4b0c-ad6c-0ca0f3e02f1c" class="">
</p><p id="f34e05ee-3428-4d13-b8ac-68e82bb949e5" class=""><strong><strong>Remove all the records that contain other weather conditions</strong></strong></p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="a73097c3-b139-4c9c-89e0-bb9c74f5e472" class="code"><code class="language-Python">WEATHER_CONDITIONS = set(weather_conditions_dict.values())

weather_measurements_aggregated_df = weather_measurements_aggregated_df \
    .filter(weather_measurements_aggregated_df[WEATHER_CONDITION_COL].isin(WEATHER_CONDITIONS))</code></pre><p id="238be62e-6b4f-405c-a91b-0342e00fd880" class="">
</p><p id="66608d08-86d1-4e9a-8d41-08c94f13e394" class="">After various step, we will get </p><table id="ccfa58f6-e64c-441f-ad8b-c648f2fc6933" class="simple-table"><tbody><tr id="ece4977b-efdd-42f4-bebf-ab4a04760666"><td id="vsnu" class="" style="width:200.3854217529297px"><strong>weather_condition</strong></td><td id="Crfh" class=""><strong>count</strong></td></tr><tr id="a3727200-b0f6-40af-8e1b-6846790f026b"><td id="vsnu" class="" style="width:200.3854217529297px">rainy</td><td id="Crfh" class="">202725</td></tr><tr id="e11d545d-fcc3-4b2b-8251-55682793e3fa"><td id="vsnu" class="" style="width:200.3854217529297px">snowy</td><td id="Crfh" class="">21283</td></tr><tr id="676cf26e-8feb-4cad-a8e6-7b6653a7db7d"><td id="vsnu" class="" style="width:200.3854217529297px">sunny</td><td id="Crfh" class="">641577</td></tr><tr id="ec2c751e-c5c6-452a-9f9e-c7b05cf91d55"><td id="vsnu" class="" style="width:200.3854217529297px">cloudy</td><td id="Crfh" class="">577842</td></tr><tr id="c9133815-dd86-475c-9792-33e3be927a23"><td id="vsnu" class="" style="width:200.3854217529297px">thunderstorm</td><td id="Crfh" class="">10852</td></tr><tr id="84468e2a-64ef-4ab4-914d-8c8a52ddc5d6"><td id="vsnu" class="" style="width:200.3854217529297px">foggy</td><td id="Crfh" class="">138707</td></tr></tbody></table><p id="4d33cc38-31cd-4474-ab7d-6790c2362e0a" class="">from the command:</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="b421b09d-5bb4-43f7-aaf9-822d2b784029" class="code"><code class="language-Python">if SLOW_OPERATIONS: weather_measurements_aggregated_df.groupBy(WEATHER_CONDITION_COL).count().show()</code></pre><p id="dea2042d-f177-480e-af5a-59ecf1512d26" class="">To clear. we plot the graph </p><figure id="349d0a2a-aba3-4f9b-8215-7072e1a28322" class="image"><a href="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled%201.png"><img style="width:1335px" src="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled%201.png"/></a></figure><p id="eb17b389-c79a-4dce-a313-2f83c23917b9" class="">
</p></div></details><details open=""><summary style="font-weight:600;font-size:1.25em;line-height:1.3;margin:0">3.2.3 <strong><strong>Undersampling procedure</strong></strong></summary><div class="indented"><p id="9c42bac4-9ebc-409e-a2ee-25dfc50a6216" class="">Following the aggregation of weather condition classes, a significant class imbalance becomes apparent. This means that some classes represent only a small portion of the total instances.</p><p id="7f25074d-7175-4d47-8be7-745c59f80b29" class="">
</p><p id="a977f09c-68f3-4da1-89aa-c262b92377ea" class="">To prevent a classifier from being overly sensitive to the majority classes and under-sensitive to the minority classes, it’s crucial to address this imbalance before feeding the data into the classifier. If left unaddressed, the classifier’s output could be biased, often resulting in the majority classes being predicted.</p><p id="15415ada-f200-426d-b44c-d02cd3811e74" class="">
</p><p id="629bbc71-05b7-45d3-b40c-f6ce69c7d77d" class="">One straightforward and effective method to handle this imbalance is undersampling. This involves reducing the number of instances in the majority classes to match the count of the minority class, thereby ensuring a more balanced dataset for classification.</p></div></details><p id="8292e57c-a9dc-472d-acfd-8f9e15b28ee4" class=""><div class="indented"><p id="122d12f6-1adb-4177-8fad-4ebdadb299c1" class="">First of all, we count occurrences of weather condition</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="8785c8cf-94f7-41b1-9e3a-30bc2a4f9744" class="code"><code class="language-Python">def count_weather_condition_occurrences(dataframe: DataFrame, class_name: str) -&gt; int:
    &#x27;&#x27;&#x27;
    Args:
        - dataframe: a `DataFrame` which contains a column `WEATHER_CONDITION_COL`
        - class_name: the class name to count the occurences of
        
    Returns:
        the total number of `class_name` occurences inside `dataframe`
    &#x27;&#x27;&#x27;
    return dataframe.filter(dataframe[WEATHER_CONDITION_COL] == class_name).count()</code></pre><p id="9137d096-5ffc-49c0-80ed-99a8eb8fa429" class="">
</p><p id="4d3e206f-5977-4bd2-9fc3-6de877c077c9" class="">The <code><strong>get_undersampling_fracs</strong></code> function takes a DataFrame of weather measurements and returns a dictionary. Each weather condition in the dictionary corresponds to a fraction that should be sampled to match the occurrences of the minority class. This helps ensure a balanced dataset for classification.</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="c85de9ae-23fa-44be-888d-111f1763f3bb" class="code"><code class="language-Python">def get_undersampling_fracs(dataframe: DataFrame) -&gt; Dict[str, float]:
    &#x27;&#x27;&#x27;
    Args:
        - dataframe: a `DataFrame` of weather measurements which contains a column `WEATHER_CONDITION_COL`
        
    Returns:
        a dictionary that goes from a weather condition to its fraction
        that should be sampled in order to match the occurences of the minority class
    &#x27;&#x27;&#x27;

    rainy_cnt = count_weather_condition_occurrences(dataframe, &#x27;rainy&#x27;)
    snowy_cnt = count_weather_condition_occurrences(dataframe, &#x27;snowy&#x27;)
    sunny_cnt = count_weather_condition_occurrences(dataframe, &#x27;sunny&#x27;)
    foggy_cnt = count_weather_condition_occurrences(dataframe, &#x27;foggy&#x27;)
    cloudy_cnt = count_weather_condition_occurrences(dataframe, &#x27;cloudy&#x27;)
    thunderstorm_cnt = count_weather_condition_occurrences(dataframe, &#x27;thunderstorm&#x27;)

    minority_class_cnt = np.min([rainy_cnt, snowy_cnt, sunny_cnt, cloudy_cnt, foggy_cnt, thunderstorm_cnt])

    return {
        &#x27;rainy&#x27;: minority_class_cnt / rainy_cnt,
        &#x27;snowy&#x27;: minority_class_cnt / snowy_cnt,
        &#x27;sunny&#x27;: minority_class_cnt / sunny_cnt,
        &#x27;foggy&#x27;: minority_class_cnt / foggy_cnt,
        &#x27;cloudy&#x27;: minority_class_cnt / cloudy_cnt,
        &#x27;thunderstorm&#x27;: minority_class_cnt / thunderstorm_cnt
    }</code></pre></div></p><p id="4e85b42b-d99b-45ea-aadb-b8f01d53861c" class="">
</p><p id="2ec9ab15-8e8b-48cd-bf10-c64dafb2a066" class=""><strong><strong>Create the new undersampled dataset</strong></strong></p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="62fe74a6-6d43-4a4d-8170-da9f82bed58f" class="code"><code class="language-Python">sampled_weather_measurements_df = ks.read_csv(SAMPLED_DATASET_PATH).to_spark() if LOAD_SAMPLED_DATASET \
                                  else not_null_weather_measurements_df.sampleBy(WEATHER_CONDITION_COL,
                                                                                 fractions=get_undersampling_fracs(not_null_weather_measurements_df),
                                                                                 seed=RANDOM_SEED)</code></pre><p id="80e0e931-89ec-4620-8146-fc3cff107be2" class="">
</p><p id="1ec1d3b4-a327-4f6e-bea8-c8b53e58340f" class="">We got</p><table id="f924a71e-3a03-4ee7-bb74-27d3c6571e1a" class="simple-table"><tbody><tr id="ce1c106e-0712-4b47-83fa-5af79735a266"><td id="Il}R" class="" style="width:308.0208435058594px"><strong>weather_condition</strong></td><td id="ZY?t" class="" style="width:243px"><strong>count</strong></td></tr><tr id="5f81cc99-3f9f-4444-b77e-ed5547d6c7cf"><td id="Il}R" class="" style="width:308.0208435058594px">rainy</td><td id="ZY?t" class="" style="width:243px">8373</td></tr><tr id="ca039171-b14f-4818-9969-64331e7f9486"><td id="Il}R" class="" style="width:308.0208435058594px">snowy</td><td id="ZY?t" class="" style="width:243px">8622</td></tr><tr id="c905d713-e47a-456d-88dd-49f30a9237f5"><td id="Il}R" class="" style="width:308.0208435058594px">sunny</td><td id="ZY?t" class="" style="width:243px">8656</td></tr><tr id="a5eae448-2b05-4e56-96dc-a8da1593590a"><td id="Il}R" class="" style="width:308.0208435058594px">cloudy</td><td id="ZY?t" class="" style="width:243px">8644</td></tr><tr id="1aa250aa-d41f-4457-a006-db316db6a3c5"><td id="Il}R" class="" style="width:308.0208435058594px">thunderstorm</td><td id="ZY?t" class="" style="width:243px">8553</td></tr><tr id="7e7d0e7d-5786-4b94-9dd5-b89ca043830a"><td id="Il}R" class="" style="width:308.0208435058594px">foggy</td><td id="ZY?t" class="" style="width:243px">8581</td></tr></tbody></table><p id="314068f5-9c77-454f-8acc-242d5283a019" class="">To clear to compare, please see undersampled graph and non-one.</p><p id="c14e3980-7a9a-4e11-9211-11d20e9f3aef" class="">
</p><figure id="68eb2a3b-62cc-4aaf-8817-b465eee31d63" class="image"><a href="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled%201.png"><img style="width:624px" src="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled%201.png"/></a></figure><p id="0623d85f-e1c1-432e-94f2-c387cc440508" class="">                             <em>             Non-undersampled graph</em></p><p id="119139b7-4655-484b-91ef-52796cb31961" class="">
</p><figure id="8a40d18a-cc43-4cc9-b1bb-74b3e1ebd46e" class="image"><a href="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled%202.png"><img style="width:1365px" src="Weather%20forecasting%20with%20PySpark%20c6df8301ae404b819a26242936f0c6fc/Untitled%202.png"/></a></figure><p id="a6493b7b-43af-47ec-bf23-3b6e8365480d" class="">                             <em>                                  Undersampled graph</em></p><h3 id="b1b3c950-f04d-448f-a760-07a68105e1fe" class="">3.2.4 Split the dataset into train and test set</h3><p id="4bbe1df2-42e3-4251-bb24-4eb062837043" class="">We randomized and split our aggregated dataset into two part, 0.8 and 0.2 for training and testing respectively</p><p id="8cc3cfc4-4206-4229-90ae-dcc0d6223a1b" class="">
</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="84045248-12c5-4ad4-bd59-3d67dcaa49ae" class="code"><code class="language-JavaScript">train_df, test_df = sampled_weather_measurements_df.randomSplit([0.8, 0.2], seed=RANDOM_SEED)</code></pre><p id="4150a2ce-e29d-4b59-8d98-43395f48edfb" class=""><div class="indented"><h2 id="e9d45182-1740-49c1-bbd2-a72e186d61d5" class="">3.3 Training and evaluating the model</h2><h3 id="195f907f-f050-41ba-88ea-2000d5484605" class="">A. Random Forest</h3><p id="b6ceac93-a687-4296-96c1-7892d178e8bf" class="">training a Machine Learning model could take up to several hours, so this simple Random Forest model, among with all the others in the Notebook, is going to be loaded from the filesystem.</p><p id="c4c6d187-cdcd-4a6b-9404-a01bb9f34c2d" class="">Set <code>LOAD_PRETRAINED_MODELS = False</code> at the beginning of this Notebook to train all the models from scratch.</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="0829075d-1aad-4340-b767-88bf24cdb28e" class="code"><code class="language-JavaScript">rnd_forest_model = RandomForestClassificationModel.load(RANDOM_FOREST_MODEL_PATH) if LOAD_PRETRAINED_MODELS \
                   else RandomForestClassifier(featuresCol=FEATURES_COL, labelCol=LABEL_COL).fit(encoded_train_df)</code></pre><p id="6e467741-fd6b-419f-841a-368f895f55fc" class=""><strong>Result: </strong><div class="indented"><p id="6cec9255-21d8-4392-b845-ecc7dfff55ee" class="">Accuracy: 0.5137359912724387 </p><p id="718f8e1d-babf-4e15-9b96-47827b801f9d" class="">Precision: 0.4913815767839824 </p><p id="8e4f60b3-7a81-4203-bf55-254164c91a57" class="">Recall: 0.5140054118534055 F1-score: 0.5024389466076965</p></div></p><h3 id="ee4aa9ab-8302-4793-8e4f-9b1311c4fd8d" class="">B. KNN</h3><p id="ad852870-3336-43e9-bb93-24cc6d47947f" class="">Since the Random Forest model took quite a long time to train (approximately 7 seconds) KNN proposed a faster way to train model with similar result</p><script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js" integrity="sha512-7Z9J3l1+EYfeaPKcGXu3MS/7T+w19WtKQY/n+xzmw4hZhJ9tyYmcUS+4QqAlzhicE5LAfMQSF3iFTK9bQdTxXg==" crossorigin="anonymous" referrerPolicy="no-referrer"></script><link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism.min.css" integrity="sha512-tN7Ec6zAFaVSG3TpNAKtk4DOHNpSwKHxxrsiw4GHKESGPs5njn/0sMCUMl2svV4wo4BK/rCP7juYz+zx+l6oeQ==" crossorigin="anonymous" referrerPolicy="no-referrer"/><pre id="df8cdf9f-5456-4606-8baf-1688237c91ed" class="code"><code class="language-JavaScript">neigh = KNeighborsClassifier(n_neighbors=18)

neigh.fit(X_train, y_train)</code></pre><p id="771da2ab-aa6c-48f3-93c3-8d9dfd4c62c1" class=""><strong>Result:</strong><div class="indented"><p id="5e8b37ea-49b5-420d-a842-f5f41adf3891" class="">Accuracy: 0.5333084298343918<br/>Precision: 0.48442858626857427<br/>Recall: 0.4828716527772194<br/>F1-score: 0.48364886652935946<br/></p><p id="9bdbc50b-92f1-4e39-a53e-813b30f53bad" class="">
</p></div></p></div></p><details open=""><summary style="font-weight:600;font-size:1.875em;line-height:1.3;margin:0">4. <strong>Improvements and Application Proposals</strong></summary><div class="indented"><p id="0acd9f8f-0b59-421d-bfca-9997f3daef4a" class="">
</p><details open=""><summary style="font-weight:600;font-size:1.5em;line-height:1.3;margin:0"><strong>Improvements:</strong></summary><div class="indented"><ol type="1" id="072f60a5-2e72-4a63-8e8c-f66f39cb0af5" class="numbered-list" start="1"><li><strong>Data Quality and Quantity:</strong> One of the main challenges in weather forecasting is the quality and quantity of data. Improving the quality of data by removing noise and outliers can enhance the accuracy of predictions. Additionally, incorporating more data sources can provide a more comprehensive view of the weather patterns.</li></ol><ol type="1" id="28b85ed9-3fff-4dc4-bc89-40c20248a573" class="numbered-list" start="2"><li><strong>Feature Engineering:</strong> The selection of features plays a crucial role in the performance of machine learning models. Experimenting with different combinations of features and creating new features based on domain knowledge can potentially improve the model’s performance.</li></ol><ol type="1" id="f8305a00-744f-468c-bfd1-7b449b3d6c35" class="numbered-list" start="3"><li><strong>Model Selection and Tuning:</strong> Different machine learning models have different strengths and weaknesses. Trying out different models and tuning their hyper parameters can help in finding the most suitable model for the task.</li></ol><ol type="1" id="5994568f-e869-4c75-b746-300391129f99" class="numbered-list" start="4"><li><strong>Ensemble Methods:</strong> Combining the predictions of multiple models can often result in better performance than any single model. Implementing ensemble methods like bagging and boosting can therefore be a potential improvement.</li></ol><p id="d21d5056-b6ae-465a-95d1-2bb13dcc3fde" class="">
</p></div></details><details open=""><summary style="font-weight:600;font-size:1.5em;line-height:1.3;margin:0"><strong>Application Proposals:</strong></summary><div class="indented"><ol type="1" id="87dfc7b1-90c5-4699-ab4d-bd373a47efe4" class="numbered-list" start="1"><li><strong>Agriculture:</strong> The improved weather forecasting model can be used in agriculture for planning farming activities like sowing, irrigation, and harvesting. This can help in increasing crop yield and reducing losses due to adverse weather conditions.</li></ol><ol type="1" id="4f12003b-7347-4f01-8d34-59680f2342ea" class="numbered-list" start="2"><li><strong>Renewable Energy:</strong> In the renewable energy sector, accurate weather forecasts can help in predicting the production of wind and solar power. This can aid in efficient grid management and reduce reliance on non-renewable sources of energy.</li></ol><ol type="1" id="14242a24-0345-4954-8780-88e5dd3fc28e" class="numbered-list" start="3"><li><strong>Disaster Management:</strong> The model can be used in disaster management for early warning of severe weather conditions like storms and floods. This can help in timely evacuation and reduce loss of life and property.</li></ol><ol type="1" id="ec4984d9-2280-4249-bff0-6225454866ae" class="numbered-list" start="4"><li><strong>Climate Research:</strong> The model can also be used in climate research for studying long-term weather patterns and understanding the impacts of climate change. This can contribute to the development of effective strategies for climate change mitigation and adaptation.</li></ol><ol type="1" id="d74192f0-93d9-4261-a32b-c0aec580f43a" class="numbered-list" start="5"><li><strong>Recreation and Leisure</strong>: The model can be used for outdoor events as event organizers use forecasts to plan concerts, sports events, and festivals. Or tourism: travelers check weather predictions for vacation planning.</li></ol><p id="45d6ffe2-86c5-4a55-9ef7-2e3f0ca09708" class="">
</p></div></details></div></details><details open=""><summary style="font-weight:600;font-size:1.875em;line-height:1.3;margin:0">5. References</summary><div class="indented"><p id="891d407a-a93c-41bb-843e-d2803eae62ae" class="">(1) Historical Hourly Weather Data 2012-2017 | Kaggle.</p><p id="44fea314-5b6e-40ab-b7c0-277efdc8fbb1" class=""><a href="https://www.kaggle.com/datasets/selfishgene/historical-hourly-weather-data">https://www.kaggle.com/datasets/selfishgene/historical-hourly-weather-data</a></p><p id="472587b5-65eb-4e5c-96c1-44afa288f094" class="">.<br/>(2) Kaggle: Your Home for Data Science.<br/></p><p id="4e939bdb-455b-4ba5-b39f-73d0796c5262" class=""><a href="https://www.kaggle.com/datasets/selfishgene/historical-hourly-weather-data/download?datasetVersionNumber=2">https://www.kaggle.com/datasets/selfishgene/historical-hourly-weather-data/download?datasetVersionNumber=2</a></p><p id="06612277-cf40-4a1f-b2c2-a11f97941ebe" class="">.<br/>(3) Python Data Analysis: How to Visualize a Kaggle Dataset with Pandas ....<br/></p><p id="4de78aed-c52a-407e-9135-9f6e3db2ebe2" class=""><a href="https://www.freecodecamp.org/news/kaggle-dataset-analysis-with-pandas-matplotlib-seaborn/">https://www.freecodecamp.org/news/kaggle-dataset-analysis-with-pandas-matplotlib-seaborn/</a></p><p id="db80ea11-1294-4f06-9b9e-29a8b0f7c110" class="">.</p><p id="258da49e-43c7-485a-834c-ede502b9f3b2" class="">(4) K-Nearest Neighbor(KNN) Algorithm</p><p id="b10cc60d-602b-4479-b081-e85db789bff6" class=""><a href="https://www.geeksforgeeks.org/k-nearest-neighbours/">https://www.geeksforgeeks.org/k-nearest-neighbours/</a></p></div></details><p id="24a1391f-d4e5-49b5-943e-f039f62dd252" class=""><div class="indented"><p id="4d4a047f-fb93-4a88-8f75-0282cc7651a4" class="">(5) Bochenek, B., &amp; Ustrnul, Z. (2022). Machine Learning in Weather Prediction and Climate Analyses—Applications and Perspectives. </p><p id="4bd2c639-a846-417a-9218-a01252288f0d" class=""><a href="https://www.mdpi.com/2073-4433/13/2/180">https://www.mdpi.com/2073-4433/13/2/180</a></p><p id="3f91120c-013c-4989-acef-9f2e86a2e683" class="">
</p><p id="0d89cc7e-a821-45f0-a7d0-3f087d2dad6d" class="">(6) Chinmaya, C. (2023). Weather Forecasting on Pyspark using Big data techniques.</p><figure id="aae17b19-0048-4769-89f4-33bab6158dba"><div class="source">https://github.com/Chinmaya083/Weather-Forecasting-using-Pyspark</div></figure><p id="9b7e5c28-9e53-472a-bed9-c25e32ea4b4f" class="">(7) Wachuka, J. (2023). Building a Weather Data Pipeline with PySpark, Prefect, and Google Cloud. </p><p id="92981c8c-1d5e-41f1-97dd-93532a0b3856" class=""><a href="https://arxiv.org/abs/2309.10808">https://arxiv.org/abs/2309.10808</a></p><p id="76cfae6d-aa71-487f-bfe9-35a3f3b6b346" class="">
</p></div></p></div></details><p id="2ede8a72-a451-4c40-9ef0-73ae49dc7cf5" class="">
</p></div></article><span class="sans" style="font-size:14px;padding-top:2em"></span></body></html>