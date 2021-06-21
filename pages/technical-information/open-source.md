---
title: Open Source
permalink: /technical-information/open-source
---

At iPaper we are fond of Open Source and we do our best to use libraries that are proven and well maintained.

Due to the nature of always keeping an eye on industry standards and most battle-hardened libraries, this list will never be static as we might switch to a more modern or up to date library later on. We do a thorough assesment when we include a new library both in the aspects of their license, their security model and last but not least how well supported is the library.

The list below includes all of the libraries we are currently using and a notation of where in our system they are used. We do not list individual packages for Microsoft .NET Framework as that is core for all of our systems to be running.

## Usage description

| Name      | Description                                                                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------------|
| Backend   | Libraries listed with this usage is used to serve all frontend related output                                     |
| Frontend  | These libraries are directly used inside of the visitors browsers                                                 |
| Services  | The libraries listed here are backend supporting services that could be nightly scheduling, PDF processing etc.   |

## Current library usage

| Name | License | Repository | Usage |
|---|---|---|---|
|AjaxMin|Apache 2.0|<http://ajaxmin.codeplex.com/>>|Backend|
|Akka|Apache 2.0|<https://github.com/akkadotnet/akka.net>|Services|
|Akka.Quartz.Actor|Apache 2.0|<https://github.com/akkadotnet/Akka.Quartz.Actor>|Services|
|Akka.Serialization.Hyperion|Apache 2.0|<https://github.com/akkadotnet/akka.net>|Services|
|AngleSharp|MIT|<https://anglesharp.github.io/>|Services|
|animejs|MIT|<https://github.com/juliangarnier/anime>|Frontend|
|Antlr|BSD|<https://github.com/antlr/antlrcs>|Backend|
|array-findindex-polyfill|MIT|<https://github.com/ryanhefner/Array.prototype.findIndex>|Frontend|
|array-from-polyfill|ISC||Frontend|
|autoprefixer|MIT|<https://github.com/postcss/autoprefixer>|Frontend|
|aws-sdk|Apache 2.0|<https://github.com/aws/aws-sdk-js>|Frontend|
|AWSSDK.CloudWatch|Apache 2.0|<https://github.com/aws/aws-sdk-net/>|Backend|
|AWSSDK.Core|Apache 2.0|<https://github.com/aws/aws-sdk-net/>|Backend Services|
|AWSSDK.S3|Apache 2.0|<https://github.com/aws/aws-sdk-net/>|Backend Services|
|AWSSDK.SimpleEmail|Apache 2.0|<https://github.com/aws/aws-sdk-net/>|Backend|
|AWSSDK.SimpleNotificationService|Apache 2.0|<https://github.com/aws/aws-sdk-net/>|Backend|
|AWSSDK.SQS|Apache 2.0|<https://github.com/aws/aws-sdk-net/>|Backend Services|
|backbone|MIT|<https://github.com/jashkenas/backbone>|Frontend|
|cache-loader|MIT|<https://github.com/webpack-contrib/cache-loader>|Frontend|
|Certes|MIT|<https://github.com/fszlin/certes>|Backend|
|clipboard|MIT|<https://github.com/zenorocha/clipboard.js>|Frontend|
|css-loader|MIT|<https://github.com/webpack-contrib/css-loader>|Frontend|
|css-vars-ponyfill|MIT|<https://jhildenbiddle@github.com/jhildenbiddle/css-vars-ponyfill>|Frontend|
|cssnano|MIT|<https://github.com/cssnano/cssnano>|Frontend|
|CsvHelper|MS-PL OR Apache 2.0|<https://joshclose.github.io/CsvHelper/>|Backend|
|custom-event-polyfill|MIT|<https://github.com/kumarharsh/custom-event-polyfill>|Frontend|
|direct-vuex|CC0-1.0|<https://github.com/paroi-tech/direct-vuex>|Frontend|
|DnsClient|Apache 2.0|<http://dnsclient.michaco.net/>|Backend|
|dotless|Apache 2.0|<https://github.com/dotless/dotless>|Backend|
|dotless.AspNetHandler|Apache 2.0|<https://github.com/dotless/dotless>|Backend|
|dotless.Core|Apache 2.0|<https://github.com/dotless/dotless>|Backend|
|EPPlus|LGPL|<https://epplussoftware.com/>|Services Backend|
|es6-object-assign|MIT|<https://github.com/rubennorte/es6-object-assign>|Frontend|
|es6-promise|MIT|<https://github.com/stefanpenner/es6-promise>|Frontend|
|es7-object-polyfill|Unlicense|<https://github.com/xpl/es7-object-polyfill>|Frontend|
|exports-loader|MIT|<https://github.com/webpack-contrib/exports-loader>|Frontend|
|Expressmapper|Apache 2.0|<http://expressmapper.org/>|Backend|
|file-loader|MIT|<https://github.com/webpack-contrib/file-loader>|Frontend|
|fork-ts-checker-webpack-plugin|MIT|<https://github.com/TypeStrong/fork-ts-checker-webpack-plugin>|Frontend|
|fscreen|MIT|<https://github.com/rafgraph/fscreen>|Frontend|
|hammerjs|MIT|<https://github.com/hammerjs/hammer.js>|Frontend|
|Hashids.net|MIT|<https://github.com/ullmark/hashids.net>|Backend|
|HtmlAgilityPack|MIT|<http://html-agility-pack.net/>|Backend Services|
|Intercom.Dotnet.Client|Apache 2.0|<https://github.com/intercom/intercom-dotnet>|Backend|
|intersection-observer|W3C-20150513|<https://github.com/w3c/IntersectionObserver>|Frontend|
|iTextSharp.LGPLv2.Core|LGPL 2.0|<https://github.com/VahidN/iTextSharp.LGPLv2.Core>|Backend Services|
|Jint|BSD-2-Clause|<https://github.com/sebastienros/jint>|Backend|
|jquery|MIT|<https://github.com/jquery/jquery>|Frontend|
|js-cookie|MIT|<https://github.com/js-cookie/js-cookie>|Frontend|
|lodash.clonedeep|MIT|<https://github.com/lodash/lodash>|Frontend|
|lodash.debounce|MIT|<https://github.com/lodash/lodash>|Frontend|
|lodash.merge|MIT|<https://github.com/lodash/lodash>|Frontend|
|lodash.mergewith|MIT|<https://github.com/lodash/lodash>|Frontend|
|Markdig|BSD-2-Clause|<https://github.com/lunet-io/markdig>|Backend|
|MaxMind.Db|Apache 2.0|<https://github.com/maxmind/MaxMind-DB-Reader-dotnet>|Backend|
|MaxMind.GeoIP2|Apache 2.0|<https://github.com/maxmind/GeoIP2-dotnet>|Backend|
|mini-css-extract-plugin|MIT|<https://github.com/webpack-contrib/mini-css-extract-plugin>|Frontend|
|Newtonsoft.Json|MIT|<https://www.newtonsoft.com/json>|Backend|
|NHttp|LGPL|<http://github.com/pvginkel/NHttp>|Services|
|number.isinteger|MIT|<https://github.com/ryanhefner/Number.isInteger>|Frontend|
|optimize-cssnano-plugin|MIT|<https://github.com/intervolga/optimize-cssnano-plugin>|Frontend|
|Pipelines.Sockets.Unofficial|MIT|<https://github.com/mgravell/Pipelines.Sockets.Unofficial>|Backend|
|player|MIT|<https://github.com/vimeo/player.js>|Frontend|
|Portable.BouncyCastle|MIT|<https://www.bouncycastle.org/csharp/>|Backend|
|portal-vue|MIT|<https://github.com/LinusBorg/portal-vue>|Frontend|
|postcss-loader|MIT|<https://github.com/postcss/postcss-loader>|Frontend|
|PreMailer.Net|MIT|<https://github.com/milkshakesoftware/PreMailer.Net>|Backend|
|promise-polyfill|MIT|<https://github.com/taylorhakes/promise-polyfill>|Frontend|
|qrcode-svg|MIT|<https://github.com/papnkukn/qrcode-svg>|Frontend|
|Quartz|Apache 2.0|<https://www.quartz-scheduler.net/>|Services|
|query-string|MIT|<https://github.com/sindresorhus/query-string>|Frontend|
|quill|BSD-3-Clause|<https://github.com/quilljs/quill>|Frontend|
|quill-delta|MIT|<https://github.com/quilljs/delta>|Frontend|
|R7Insight.Core|MIT|<https://github.com/rapid7/r7insight_dotnet/>|Services Backend|
|RazorEngine|Apache 2.0|<https://github.com/Antaris/RazorEngine>|Backend|
|RestSharp|Apache 2.0|<http://restsharp.org/>|Backend|
|sass|MIT|<https://github.com/sass/dart-sass>|Frontend|
|sass-loader|MIT|<https://github.com/webpack-contrib/sass-loader>|Frontend|
|sortablejs|MIT|<https://github.com/SortableJS/Sortable>|Frontend|
|StackExchange.Redis|MIT|<https://github.com/StackExchange/StackExchange.Redis/>|Backend|
|string.prototype.startswith|MIT|<https://github.com/mathiasbynens/String.prototype.startsWith>|Frontend|
|Stripe.net|Apache 2.0|<https://github.com/stripe/stripe-dotnet>|Backend|
|svgo|MIT|<https://github.com/svg/svgo>|Frontend|
|svgo-loader|MIT|<https://github.com/pozadi/svgo-loader>|Frontend|
|terser-webpack-plugin|MIT|<https://github.com/webpack-contrib/terser-webpack-plugin>|Frontend|
|tinycolor2|MIT|<https://bgrinshub.com/TinyColor>|Frontend|
|Topshelf|Apache 2.0|<https://github.com/Topshelf/Topshelf>|Services|
|ts-keycode-enum|MIT|<https://github.com/nfriend/ts-keycode-enum>|Frontend|
|ts-loader|MIT|<https://github.com/TypeStrong/ts-loader>|Frontend|
|tslib|Apache 2.0|<https://github.com/Microsoft/tslib>|Frontend|
|tween.js|MIT|<https://github.com/tweenjs/tween.js>|Frontend|
|TwoFactorAuth.Net|MIT|<https://github.com/RobThree/TwoFactorAuth.Net>|Backend|
|typescript|Apache 2.0|<https://github.com/Microsoft/TypeScript>|Frontend|
|underscore|MIT|<https://github.com/jashkenas/underscore>|Frontend|
|unQuery|MIT|<https://github.com/improvedk/unQuery>|Backend Services|
|uuid|MIT|<https://github.com/uuidjs/uuid>|Frontend|
|vue|MIT|<https://github.com/vuejs/vue>|Frontend|
|vue-class-component|MIT|<https://github.com/vuejs/vue-class-component>|Frontend|
|vue-implicit-css-modules|MIT|<https://github.com/AjiTae/vue-implicit-css-modules>|Frontend|
|vue-loader|MIT|<https://github.com/vuejs/vue-loader>|Frontend|
|vue-property-decorator|MIT|<https://github.com/kaorun343/vue-property-decorator>|Frontend|
|vue-router|MIT|<https://github.com/vuejs/vue-router>|Frontend|
|vue-style-loader|MIT|<https://github.com/vuejs/vue-style-loader>|Frontend|
|vue-svg-loader|MIT|<https://github.com/visualfanatic/vue-svg-loader>|Frontend|
|vue-template-compiler|MIT|<https://github.com/vuejs/vue>>|Frontend|
|vuedraggable|MIT|<https://github.com/SortableJS/Vue.Draggable>>|Frontend|
|vuex|MIT|<https://github.com/vuejs/vuex>>|Frontend|
|vuex-class|MIT|<https://github.com/ktsn/vuex-class>>|Frontend|
|weakmap-polyfill|MIT|<https://github.com/polygonplanet/weakmap-polyfill>>|Frontend|
|webfontloader|Apache 2.0|<https://github.com/typekit/webfontloader>>|Frontend|
|webpack|MIT|<https://github.com/webpack/webpack>>|Frontend|
|whatwg-fetch|MIT|<https://github.com/github/fetch>>|Frontend|
|zlib.net|BSD-Style|<http://www.componentace.com/zlib_.NET.htm>>|Backend|
