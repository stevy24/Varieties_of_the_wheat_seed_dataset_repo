<!DOCTYPE html>
<!-- saved from url=(0134)http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb -->
<html lang="fr-fr"><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    

    <title>Varieties_of_the_wheat_seed_dataset</title>
    
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <link rel="stylesheet" href="./README_files/jquery-ui.min.css" type="text/css">
    <link rel="stylesheet" href="./README_files/jquery.typeahead.min.css" type="text/css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    


<script type="text/javascript" src="./README_files/MathJax.js.download" charset="utf-8"></script>

<script type="text/javascript">
// MathJax disabled, set as null to distingish from *missing* MathJax,
// where it will be undefined, and should prompt a dialog later.
window.mathjax_url = "/static/components/MathJax/MathJax.js";
</script>

<link rel="stylesheet" href="./README_files/bootstrap-tour.min.css" type="text/css">
<link rel="stylesheet" href="./README_files/codemirror.css">


    <link rel="stylesheet" href="./README_files/style.min.css" type="text/css">
    

<link rel="stylesheet" href="./README_files/override.css" type="text/css">
<link rel="stylesheet" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb" id="kernel-css" type="text/css">


    <link rel="stylesheet" href="./README_files/custom.css" type="text/css">
    <script src="./README_files/promise.min.js.download" type="text/javascript" charset="utf-8"></script>
    <script src="./README_files/index.js.download" type="text/javascript"></script>
    <script src="./README_files/index.js(1).download" type="text/javascript"></script>
    <script src="./README_files/index.js(2).download" type="text/javascript"></script>
    <script src="./README_files/require.js.download" type="text/javascript" charset="utf-8"></script>
    <script>
      require.config({
          
          urlArgs: "v=20190227082127",
          
          baseUrl: '/static/',
          paths: {
            'auth/js/main': 'auth/js/main.min',
            custom : '/custom',
            nbextensions : '/nbextensions',
            kernelspecs : '/kernelspecs',
            underscore : 'components/underscore/underscore-min',
            backbone : 'components/backbone/backbone-min',
            jed: 'components/jed/jed',
            jquery: 'components/jquery/jquery.min',
            json: 'components/requirejs-plugins/src/json',
            text: 'components/requirejs-text/text',
            bootstrap: 'components/bootstrap/js/bootstrap.min',
            bootstraptour: 'components/bootstrap-tour/build/js/bootstrap-tour.min',
            'jquery-ui': 'components/jquery-ui/ui/minified/jquery-ui.min',
            moment: 'components/moment/min/moment-with-locales',
            codemirror: 'components/codemirror',
            termjs: 'components/xterm.js/xterm',
            typeahead: 'components/jquery-typeahead/dist/jquery.typeahead.min',
          },
          map: { // for backward compatibility
              "*": {
                  "jqueryui": "jquery-ui",
              }
          },
          shim: {
            typeahead: {
              deps: ["jquery"],
              exports: "typeahead"
            },
            underscore: {
              exports: '_'
            },
            backbone: {
              deps: ["underscore", "jquery"],
              exports: "Backbone"
            },
            bootstrap: {
              deps: ["jquery"],
              exports: "bootstrap"
            },
            bootstraptour: {
              deps: ["bootstrap"],
              exports: "Tour"
            },
            "jquery-ui": {
              deps: ["jquery"],
              exports: "$"
            }
          },
          waitSeconds: 30,
      });

      require.config({
          map: {
              '*':{
                'contents': 'services/contents',
              }
          }
      });

      // error-catching custom.js shim.
      define("custom", function (require, exports, module) {
          try {
              var custom = require('custom/custom');
              console.debug('loaded custom.js');
              return custom;
          } catch (e) {
              console.error("error loading custom.js", e);
              return {};
          }
      })

    document.nbjs_translations = {"domain": "nbjs", "locale_data": {"nbjs": {"": {"domain": "nbjs"}}}};
    document.documentElement.lang = navigator.language.toLowerCase();
    </script>

    
    

<script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="services/contents" src="./README_files/contents.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="custom/custom" src="./README_files/custom.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/plotlywidget/extension" src="./README_files/extension.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/jupyter-js-widgets/extension" src="./README_files/extension.js(1).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/nbextensions_configurator/config_menu/main" src="./README_files/main.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/contrib_nbextensions_help_item/main" src="./README_files/main.js(1).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/varInspector/main" src="./README_files/main.js(2).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/code_prettify" src="./README_files/code_prettify.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/collapsible_headings/main" src="./README_files/main.js(3).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/toc2/main" src="./README_files/main.js(4).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/main" src="./README_files/main.js(5).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/export_embedded/main" src="./README_files/main.js(6).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/autopep8" src="./README_files/autopep8.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_font_size/code_font_size" src="./README_files/code_font_size.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/gist_it/main" src="./README_files/main.js(7).download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/python-markdown/main" src="./README_files/main.js(8).download"></script><style type="text/css">.MathJax_Hover_Frame {border-radius: .25em; -webkit-border-radius: .25em; -moz-border-radius: .25em; -khtml-border-radius: .25em; box-shadow: 0px 0px 15px #83A; -webkit-box-shadow: 0px 0px 15px #83A; -moz-box-shadow: 0px 0px 15px #83A; -khtml-box-shadow: 0px 0px 15px #83A; border: 1px solid #A6D ! important; display: inline-block; position: absolute}
.MathJax_Menu_Button .MathJax_Hover_Arrow {position: absolute; cursor: pointer; display: inline-block; border: 2px solid #AAA; border-radius: 4px; -webkit-border-radius: 4px; -moz-border-radius: 4px; -khtml-border-radius: 4px; font-family: 'Courier New',Courier; font-size: 9px; color: #F0F0F0}
.MathJax_Menu_Button .MathJax_Hover_Arrow span {display: block; background-color: #AAA; border: 1px solid; border-radius: 3px; line-height: 0; padding: 4px}
.MathJax_Hover_Arrow:hover {color: white!important; border: 2px solid #CCC!important}
.MathJax_Hover_Arrow:hover span {background-color: #CCC!important}
</style><style type="text/css">#MathJax_About {position: fixed; left: 50%; width: auto; text-align: center; border: 3px outset; padding: 1em 2em; background-color: #DDDDDD; color: black; cursor: default; font-family: message-box; font-size: 120%; font-style: normal; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; z-index: 201; border-radius: 15px; -webkit-border-radius: 15px; -moz-border-radius: 15px; -khtml-border-radius: 15px; box-shadow: 0px 10px 20px #808080; -webkit-box-shadow: 0px 10px 20px #808080; -moz-box-shadow: 0px 10px 20px #808080; -khtml-box-shadow: 0px 10px 20px #808080; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
#MathJax_About.MathJax_MousePost {outline: none}
.MathJax_Menu {position: absolute; background-color: white; color: black; width: auto; padding: 2px; border: 1px solid #CCCCCC; margin: 0; cursor: default; font: menu; text-align: left; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; z-index: 201; box-shadow: 0px 10px 20px #808080; -webkit-box-shadow: 0px 10px 20px #808080; -moz-box-shadow: 0px 10px 20px #808080; -khtml-box-shadow: 0px 10px 20px #808080; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
.MathJax_MenuItem {padding: 2px 2em; background: transparent}
.MathJax_MenuArrow {position: absolute; right: .5em; padding-top: .25em; color: #666666; font-size: .75em}
.MathJax_MenuActive .MathJax_MenuArrow {color: white}
.MathJax_MenuArrow.RTL {left: .5em; right: auto}
.MathJax_MenuCheck {position: absolute; left: .7em}
.MathJax_MenuCheck.RTL {right: .7em; left: auto}
.MathJax_MenuRadioCheck {position: absolute; left: 1em}
.MathJax_MenuRadioCheck.RTL {right: 1em; left: auto}
.MathJax_MenuLabel {padding: 2px 2em 4px 1.33em; font-style: italic}
.MathJax_MenuRule {border-top: 1px solid #CCCCCC; margin: 4px 1px 0px}
.MathJax_MenuDisabled {color: GrayText}
.MathJax_MenuActive {background-color: Highlight; color: HighlightText}
.MathJax_MenuDisabled:focus, .MathJax_MenuLabel:focus {background-color: #E8E8E8}
.MathJax_ContextMenu:focus {outline: none}
.MathJax_ContextMenu .MathJax_MenuItem:focus {outline: none}
#MathJax_AboutClose {top: .2em; right: .2em}
.MathJax_Menu .MathJax_MenuClose {top: -10px; left: -10px}
.MathJax_MenuClose {position: absolute; cursor: pointer; display: inline-block; border: 2px solid #AAA; border-radius: 18px; -webkit-border-radius: 18px; -moz-border-radius: 18px; -khtml-border-radius: 18px; font-family: 'Courier New',Courier; font-size: 24px; color: #F0F0F0}
.MathJax_MenuClose span {display: block; background-color: #AAA; border: 1.5px solid; border-radius: 18px; -webkit-border-radius: 18px; -moz-border-radius: 18px; -khtml-border-radius: 18px; line-height: 0; padding: 8px 0 6px}
.MathJax_MenuClose:hover {color: white!important; border: 2px solid #CCC!important}
.MathJax_MenuClose:hover span {background-color: #CCC!important}
.MathJax_MenuClose:hover:focus {outline: none}
</style><style type="text/css">.MathJax_Preview .MJXf-math {color: inherit!important}
</style><style type="text/css">.MJX_Assistive_MathML {position: absolute!important; top: 0; left: 0; clip: rect(1px, 1px, 1px, 1px); padding: 1px 0 0 0!important; border: 0!important; height: 1px!important; width: 1px!important; overflow: hidden!important; display: block!important; -webkit-touch-callout: none; -webkit-user-select: none; -khtml-user-select: none; -moz-user-select: none; -ms-user-select: none; user-select: none}
.MJX_Assistive_MathML.MJX_Assistive_MathML_Block {width: 100%!important}
</style><style type="text/css">#MathJax_Zoom {position: absolute; background-color: #F0F0F0; overflow: auto; display: block; z-index: 301; padding: .5em; border: 1px solid black; margin: 0; font-weight: normal; font-style: normal; text-align: left; text-indent: 0; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; -webkit-box-sizing: content-box; -moz-box-sizing: content-box; box-sizing: content-box; box-shadow: 5px 5px 15px #AAAAAA; -webkit-box-shadow: 5px 5px 15px #AAAAAA; -moz-box-shadow: 5px 5px 15px #AAAAAA; -khtml-box-shadow: 5px 5px 15px #AAAAAA; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true')}
#MathJax_ZoomOverlay {position: absolute; left: 0; top: 0; z-index: 300; display: inline-block; width: 100%; height: 100%; border: 0; padding: 0; margin: 0; background-color: white; opacity: 0; filter: alpha(opacity=0)}
#MathJax_ZoomFrame {position: relative; display: inline-block; height: 0; width: 0}
#MathJax_ZoomEventTrap {position: absolute; left: 0; top: 0; z-index: 302; display: inline-block; border: 0; padding: 0; margin: 0; background-color: white; opacity: 0; filter: alpha(opacity=0)}
</style><style type="text/css">.MathJax_Preview {color: #888}
#MathJax_Message {position: fixed; left: 1em; bottom: 1.5em; background-color: #E6E6E6; border: 1px solid #959595; margin: 0px; padding: 2px 8px; z-index: 102; color: black; font-size: 80%; width: auto; white-space: nowrap}
#MathJax_MSIE_Frame {position: absolute; top: 0; left: 0; width: 0px; z-index: 101; border: 0px; margin: 0px; padding: 0px}
.MathJax_Error {color: #CC0000; font-style: italic}
</style><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/code_prettify/kernel_exec_on_cell" src="./README_files/kernel_exec_on_cell.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/toc2/toc2" src="./README_files/toc2.js.download"></script><link type="text/css" rel="stylesheet" href="./README_files/main.css"><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/foldcode" src="./README_files/foldcode.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/foldgutter" src="./README_files/foldgutter.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/brace-fold" src="./README_files/brace-fold.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="codemirror/addon/fold/indent-fold" src="./README_files/indent-fold.js.download"></script><link id="collapsible_headings_css" rel="stylesheet" type="text/css" href="./README_files/main(1).css"><link type="text/css" rel="stylesheet" href="./README_files/main(2).css"><style type="text/css">div.MathJax_MathML {text-align: center; margin: .75em 0px; display: block!important}
.MathJax_MathML {font-style: normal; font-weight: normal; line-height: normal; font-size: 100%; font-size-adjust: none; text-indent: 0; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0; min-height: 0; border: 0; padding: 0; margin: 0}
span.MathJax_MathML {display: inline!important}
.MathJax_mmlExBox {display: block!important; overflow: hidden; height: 1px; width: 60ex; min-height: 0; max-height: none; padding: 0; border: 0; margin: 0}
[class="MJX-tex-oldstyle"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB}
[class="MJX-tex-oldstyle-bold"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB; font-weight: bold}
[class="MJX-tex-caligraphic"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB}
[class="MJX-tex-caligraphic-bold"] {font-family: MathJax_Caligraphic, MathJax_Caligraphic-WEB; font-weight: bold}
@font-face /*1*/ {font-family: MathJax_Caligraphic-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Caligraphic-Regular.otf')}
@font-face /*2*/ {font-family: MathJax_Caligraphic-WEB; font-weight: bold; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Caligraphic-Bold.otf')}
[mathvariant="double-struck"] {font-family: MathJax_AMS, MathJax_AMS-WEB}
[mathvariant="script"] {font-family: MathJax_Script, MathJax_Script-WEB}
[mathvariant="fraktur"] {font-family: MathJax_Fraktur, MathJax_Fraktur-WEB}
[mathvariant="bold-script"] {font-family: MathJax_Script, MathJax_Caligraphic-WEB; font-weight: bold}
[mathvariant="bold-fraktur"] {font-family: MathJax_Fraktur, MathJax_Fraktur-WEB; font-weight: bold}
[mathvariant="monospace"] {font-family: monospace}
[mathvariant="sans-serif"] {font-family: sans-serif}
[mathvariant="bold-sans-serif"] {font-family: sans-serif; font-weight: bold}
[mathvariant="sans-serif-italic"] {font-family: sans-serif; font-style: italic}
[mathvariant="sans-serif-bold-italic"] {font-family: sans-serif; font-style: italic; font-weight: bold}
@font-face /*3*/ {font-family: MathJax_AMS-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_AMS-Regular.otf')}
@font-face /*4*/ {font-family: MathJax_Script-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Script-Regular.otf')}
@font-face /*5*/ {font-family: MathJax_Fraktur-WEB; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Fraktur-Regular.otf')}
@font-face /*6*/ {font-family: MathJax_Fraktur-WEB; font-weight: bold; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/TeX/otf/MathJax_Fraktur-Bold.otf')}
</style><style type="text/css">.MJXp-script {font-size: .8em}
.MJXp-right {-webkit-transform-origin: right; -moz-transform-origin: right; -ms-transform-origin: right; -o-transform-origin: right; transform-origin: right}
.MJXp-bold {font-weight: bold}
.MJXp-italic {font-style: italic}
.MJXp-scr {font-family: MathJax_Script,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-frak {font-family: MathJax_Fraktur,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-sf {font-family: MathJax_SansSerif,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-cal {font-family: MathJax_Caligraphic,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-mono {font-family: MathJax_Typewriter,'Times New Roman',Times,STIXGeneral,serif}
.MJXp-largeop {font-size: 150%}
.MJXp-largeop.MJXp-int {vertical-align: -.2em}
.MJXp-math {display: inline-block; line-height: 1.2; text-indent: 0; font-family: 'Times New Roman',Times,STIXGeneral,serif; white-space: nowrap; border-collapse: collapse}
.MJXp-display {display: block; text-align: center; margin: 1em 0}
.MJXp-math span {display: inline-block}
.MJXp-box {display: block!important; text-align: center}
.MJXp-box:after {content: " "}
.MJXp-rule {display: block!important; margin-top: .1em}
.MJXp-char {display: block!important}
.MJXp-mo {margin: 0 .15em}
.MJXp-mfrac {margin: 0 .125em; vertical-align: .25em}
.MJXp-denom {display: inline-table!important; width: 100%}
.MJXp-denom > * {display: table-row!important}
.MJXp-surd {vertical-align: top}
.MJXp-surd > * {display: block!important}
.MJXp-script-box > *  {display: table!important; height: 50%}
.MJXp-script-box > * > * {display: table-cell!important; vertical-align: top}
.MJXp-script-box > *:last-child > * {vertical-align: bottom}
.MJXp-script-box > * > * > * {display: block!important}
.MJXp-mphantom {visibility: hidden}
.MJXp-munderover {display: inline-table!important}
.MJXp-over {display: inline-block!important; text-align: center}
.MJXp-over > * {display: block!important}
.MJXp-munderover > * {display: table-row!important}
.MJXp-mtable {vertical-align: .25em; margin: 0 .125em}
.MJXp-mtable > * {display: inline-table!important; vertical-align: middle}
.MJXp-mtr {display: table-row!important}
.MJXp-mtd {display: table-cell!important; text-align: center; padding: .5em 0 0 .5em}
.MJXp-mtr > .MJXp-mtd:first-child {padding-left: 0}
.MJXp-mtr:first-child > .MJXp-mtd {padding-top: 0}
.MJXp-mlabeledtr {display: table-row!important}
.MJXp-mlabeledtr > .MJXp-mtd:first-child {padding-left: 0}
.MJXp-mlabeledtr:first-child > .MJXp-mtd {padding-top: 0}
.MJXp-merror {background-color: #FFFF88; color: #CC0000; border: 1px solid #CC0000; padding: 1px 3px; font-style: normal; font-size: 90%}
.MJXp-scale0 {-webkit-transform: scaleX(.0); -moz-transform: scaleX(.0); -ms-transform: scaleX(.0); -o-transform: scaleX(.0); transform: scaleX(.0)}
.MJXp-scale1 {-webkit-transform: scaleX(.1); -moz-transform: scaleX(.1); -ms-transform: scaleX(.1); -o-transform: scaleX(.1); transform: scaleX(.1)}
.MJXp-scale2 {-webkit-transform: scaleX(.2); -moz-transform: scaleX(.2); -ms-transform: scaleX(.2); -o-transform: scaleX(.2); transform: scaleX(.2)}
.MJXp-scale3 {-webkit-transform: scaleX(.3); -moz-transform: scaleX(.3); -ms-transform: scaleX(.3); -o-transform: scaleX(.3); transform: scaleX(.3)}
.MJXp-scale4 {-webkit-transform: scaleX(.4); -moz-transform: scaleX(.4); -ms-transform: scaleX(.4); -o-transform: scaleX(.4); transform: scaleX(.4)}
.MJXp-scale5 {-webkit-transform: scaleX(.5); -moz-transform: scaleX(.5); -ms-transform: scaleX(.5); -o-transform: scaleX(.5); transform: scaleX(.5)}
.MJXp-scale6 {-webkit-transform: scaleX(.6); -moz-transform: scaleX(.6); -ms-transform: scaleX(.6); -o-transform: scaleX(.6); transform: scaleX(.6)}
.MJXp-scale7 {-webkit-transform: scaleX(.7); -moz-transform: scaleX(.7); -ms-transform: scaleX(.7); -o-transform: scaleX(.7); transform: scaleX(.7)}
.MJXp-scale8 {-webkit-transform: scaleX(.8); -moz-transform: scaleX(.8); -ms-transform: scaleX(.8); -o-transform: scaleX(.8); transform: scaleX(.8)}
.MJXp-scale9 {-webkit-transform: scaleX(.9); -moz-transform: scaleX(.9); -ms-transform: scaleX(.9); -o-transform: scaleX(.9); transform: scaleX(.9)}
.MathJax_PHTML .noError {vertical-align: ; font-size: 90%; text-align: left; color: black; padding: 1px 3px; border: 1px solid}
</style><style id="collapsible_headings_indent_css">.collapsible_headings_toggle .h1 { margin-right: 40px; }
.collapsible_headings_toggle .h2 { margin-right: 32px; }
.collapsible_headings_toggle .h3 { margin-right: 24px; }
.collapsible_headings_toggle .h4 { margin-right: 16px; }
.collapsible_headings_toggle .h5 { margin-right: 8px; }
.collapsible_headings_toggle .h6 { margin-right: 0px; }</style><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/varInspector/jquery.tablesorter.min" src="./README_files/jquery.tablesorter.min.js.download"></script><style type="text/css">.MathJax_Display {text-align: center; margin: 0; position: relative; display: block!important; text-indent: 0; max-width: none; max-height: none; min-width: 0; min-height: 0; width: 100%}
.MathJax .merror {background-color: #FFFF88; color: #CC0000; border: 1px solid #CC0000; padding: 1px 3px; font-style: normal; font-size: 90%}
.MathJax .MJX-monospace {font-family: monospace}
.MathJax .MJX-sans-serif {font-family: sans-serif}
#MathJax_Tooltip {background-color: InfoBackground; color: InfoText; border: 1px solid black; box-shadow: 2px 2px 5px #AAAAAA; -webkit-box-shadow: 2px 2px 5px #AAAAAA; -moz-box-shadow: 2px 2px 5px #AAAAAA; -khtml-box-shadow: 2px 2px 5px #AAAAAA; filter: progid:DXImageTransform.Microsoft.dropshadow(OffX=2, OffY=2, Color='gray', Positive='true'); padding: 3px 4px; z-index: 401; position: absolute; left: 0; top: 0; width: auto; height: auto; display: none}
.MathJax {display: inline; font-style: normal; font-weight: normal; line-height: normal; font-size: 100%; font-size-adjust: none; text-indent: 0; text-align: left; text-transform: none; letter-spacing: normal; word-spacing: normal; word-wrap: normal; white-space: nowrap; float: none; direction: ltr; max-width: none; max-height: none; min-width: 0; min-height: 0; border: 0; padding: 0; margin: 0}
.MathJax:focus, body :focus .MathJax {display: inline-table}
.MathJax.MathJax_FullWidth {text-align: center; display: table-cell!important; width: 10000em!important}
.MathJax img, .MathJax nobr, .MathJax a {border: 0; padding: 0; margin: 0; max-width: none; max-height: none; min-width: 0; min-height: 0; vertical-align: 0; line-height: normal; text-decoration: none}
img.MathJax_strut {border: 0!important; padding: 0!important; margin: 0!important; vertical-align: 0!important}
.MathJax span {display: inline; position: static; border: 0; padding: 0; margin: 0; vertical-align: 0; line-height: normal; text-decoration: none; box-sizing: content-box}
.MathJax nobr {white-space: nowrap!important}
.MathJax img {display: inline!important; float: none!important}
.MathJax * {transition: none; -webkit-transition: none; -moz-transition: none; -ms-transition: none; -o-transition: none}
.MathJax_Processing {visibility: hidden; position: fixed; width: 0; height: 0; overflow: hidden}
.MathJax_Processed {display: none!important}
.MathJax_ExBox {display: block!important; overflow: hidden; width: 1px; height: 60ex; min-height: 0; max-height: none}
.MathJax .MathJax_EmBox {display: block!important; overflow: hidden; width: 1px; height: 60em; min-height: 0; max-height: none}
.MathJax_LineBox {display: table!important}
.MathJax_LineBox span {display: table-cell!important; width: 10000em!important; min-width: 0; max-width: none; padding: 0; border: 0; margin: 0}
.MathJax .MathJax_HitBox {cursor: text; background: white; opacity: 0; filter: alpha(opacity=0)}
.MathJax .MathJax_HitBox * {filter: none; opacity: 1; background: transparent}
#MathJax_Tooltip * {filter: none; opacity: 1; background: transparent}
@font-face {font-family: MathJax_Blank; src: url('about:blank')}
.MathJax .noError {vertical-align: ; font-size: 90%; text-align: left; color: black; padding: 1px 3px; border: 1px solid}
</style><link type="text/css" rel="stylesheet" href="./README_files/main(3).css"><link type="text/css" rel="stylesheet" href="./README_files/foldgutter.css"><link type="text/css" rel="stylesheet" href="./README_files/foldgutter(1).css"><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/firstline-fold" src="./README_files/firstline-fold.js.download"></script><script type="text/javascript" charset="utf-8" async="" data-requirecontext="_" data-requiremodule="nbextensions/codefolding/magic-fold" src="./README_files/magic-fold.js.download"></script><style type="text/css">/*
 * Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

/* Override the correction for the prompt area in https://github.com/jupyter/notebook/blob/dd41d9fd5c4f698bd7468612d877828a7eeb0e7a/IPython/html/static/notebook/less/outputarea.less#L110 */

.jupyter-widgets-output-area div.output_subarea {
    max-width: 100%;
}

/* Work-around for the bug fixed in https://github.com/jupyter/notebook/pull/2961 */

.jupyter-widgets-output-area > .out_prompt_overlay {
    display: none;
}
</style><style type="text/css">/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-Widget {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: relative;
  overflow: hidden;
  cursor: default;
}
.p-Widget.p-mod-hidden {
  display: none !important;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-CommandPalette {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-CommandPalette-search {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-content {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}
.p-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.p-CommandPalette-item {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-CommandPalette-itemIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-itemContent {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
}
.p-CommandPalette-itemShortcut {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-DockPanel {
  z-index: 0;
}
.p-DockPanel-widget {
  z-index: 0;
}
.p-DockPanel-tabBar {
  z-index: 1;
}
.p-DockPanel-handle {
  z-index: 2;
}
.p-DockPanel-handle.p-mod-hidden {
  display: none !important;
}
.p-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}
.p-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}
.p-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}
.p-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  -webkit-transform: translateX(-50%);
          transform: translateX(-50%);
}
.p-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  -webkit-transform: translateY(-50%);
          transform: translateY(-50%);
}
.p-DockPanel-overlay {
  z-index: 3;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  pointer-events: none;
}
.p-DockPanel-overlay.p-mod-hidden {
  display: none !important;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}
.p-Menu-item {
  display: table-row;
}
.p-Menu-item.p-mod-hidden,
.p-Menu-item.p-mod-collapsed {
  display: none !important;
}
.p-Menu-itemIcon,
.p-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}
.p-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}
.p-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-MenuBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  list-style-type: none;
}
.p-MenuBar-item {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
}
.p-MenuBar-itemIcon,
.p-MenuBar-itemLabel {
  display: inline-block;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-ScrollBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-ScrollBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-ScrollBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-ScrollBar-button {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-ScrollBar-track {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: relative;
  overflow: hidden;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
}
.p-ScrollBar-thumb {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  position: absolute;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-SplitPanel-child {
  z-index: 0;
}
.p-SplitPanel-handle {
  z-index: 1;
}
.p-SplitPanel-handle.p-mod-hidden {
  display: none !important;
}
.p-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle {
  cursor: ew-resize;
}
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle {
  cursor: ns-resize;
}
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  -webkit-transform: translateX(-50%);
          transform: translateX(-50%);
}
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  -webkit-transform: translateY(-50%);
          transform: translateY(-50%);
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-TabBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.p-TabBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-TabBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-TabBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  list-style-type: none;
}
.p-TabBar[data-orientation='horizontal'] > .p-TabBar-content {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}
.p-TabBar[data-orientation='vertical'] > .p-TabBar-content {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.p-TabBar-tab {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  overflow: hidden;
}
.p-TabBar-tabIcon,
.p-TabBar-tabCloseIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}
.p-TabBar-tabLabel {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}
.p-TabBar-tab.p-mod-hidden {
  display: none !important;
}
.p-TabBar.p-mod-dragging .p-TabBar-tab {
  position: relative;
}
.p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab {
  left: 0;
  -webkit-transition: left 150ms ease;
  transition: left 150ms ease;
}
.p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab {
  top: 0;
  -webkit-transition: top 150ms ease;
  transition: top 150ms ease;
}
.p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging {
  -webkit-transition: none;
  transition: none;
}
/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/
.p-TabPanel-tabBar {
  z-index: 1;
}
.p-TabPanel-stackedPanel {
  z-index: 0;
}
</style><style type="text/css">/* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 .jupyter-widgets-disconnected::before {
    content: "\F127"; /* chain-broken */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #d9534f;
    padding: 3px;
    -ms-flex-item-align: start;
        align-self: flex-start;
}
</style><style type="text/css">/* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 /* We import all of these together in a single css file because the Webpack
loader sees only one file at a time. This allows postcss to see the variable
definitions when they are used. */

 /*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

 /*
This file is copied from the JupyterLab project to define default styling for
when the widget styling is compiled down to eliminate CSS variables. We make one
change - we comment out the font import below.
*/

 /**
 * The material design colors are adapted from google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 * https://github.com/danlevan/google-material-color/blob/f67ca5f4028b2f1b34862f64b0ca67323f91b088/dist/palette.var.css
 *
 * The license for the material design color CSS variables is as follows (see
 * https://github.com/danlevan/google-material-color/blob/f67ca5f4028b2f1b34862f64b0ca67323f91b088/LICENSE)
 *
 * The MIT License (MIT)
 *
 * Copyright (c) 2014 Dan Le Van
 *
 * Permission is hereby granted, free of charge, to any person obtaining a copy
 * of this software and associated documentation files (the "Software"), to deal
 * in the Software without restriction, including without limitation the rights
 * to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 * copies of the Software, and to permit persons to whom the Software is
 * furnished to do so, subject to the following conditions:
 *
 * The above copyright notice and this permission notice shall be included in
 * all copies or substantial portions of the Software.
 *
 * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 * IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 * FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 * AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 * LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 * OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
 * SOFTWARE.
 */

 /*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

 /*
 * Optional monospace font for input/output prompt.
 */

 /* Commented out in ipywidgets since we don't need it. */

 /* @import url('https://fonts.googleapis.com/css?family=Roboto+Mono'); */

 /*
 * Added for compabitility with output area
 */

 :root {

  /* Borders

  The following variables, specify the visual styling of borders in JupyterLab.
   */

  /* UI Fonts

  The UI font CSS variables are used for the typography all of the JupyterLab
  user interface elements that are not directly user generated content.
  */ /* Base font size */ /* Ensures px perfect FontAwesome icons */

  /* Use these font colors against the corresponding main layout colors.
     In a light theme, these go from dark to light.
  */

  /* Use these against the brand/accent/warn/error colors.
     These will typically go from light to darker, in both a dark and light theme
   */

  /* Content Fonts

  Content font variables are used for typography of user generated content.
  */ /* Base font size */


  /* Layout

  The following are the main layout colors use in JupyterLab. In a light
  theme these would go from light to dark.
  */

  /* Brand/accent */

  /* State colors (warn, error, success, info) */

  /* Cell specific styles */
  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */

  /* Notebook specific styles */

  /* Console specific styles */

  /* Toolbar specific styles */
}

 /* Copyright (c) Jupyter Development Team.
 * Distributed under the terms of the Modified BSD License.
 */

 /*
 * We assume that the CSS variables in
 * https://github.com/jupyterlab/jupyterlab/blob/master/src/default-theme/variables.css
 * have been defined.
 */

 /* This file has code derived from PhosphorJS CSS files, as noted below. The license for this PhosphorJS code is:

Copyright (c) 2014-2017, PhosphorJS Contributors
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of the copyright holder nor the names of its
  contributors may be used to endorse or promote products derived from
  this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

*/

 /*
 * The following section is derived from https://github.com/phosphorjs/phosphor/blob/23b9d075ebc5b73ab148b6ebfc20af97f85714c4/packages/widgets/style/tabbar.css 
 * We've scoped the rules so that they are consistent with exactly our code.
 */

 .jupyter-widgets.widget-tab > .p-TabBar {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='horizontal'] {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='vertical'] {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar > .p-TabBar-content {
  margin: 0;
  padding: 0;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  list-style-type: none;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='horizontal'] > .p-TabBar-content {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
}

 .jupyter-widgets.widget-tab > .p-TabBar[data-orientation='vertical'] > .p-TabBar-content {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
      -ms-flex-direction: row;
          flex-direction: row;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  overflow: hidden;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabIcon,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabCloseIcon {
  -webkit-box-flex: 0;
      -ms-flex: 0 0 auto;
          flex: 0 0 auto;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabLabel {
  -webkit-box-flex: 1;
      -ms-flex: 1 1 auto;
          flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-hidden {
  display: none !important;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging .p-TabBar-tab {
  position: relative;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab {
  left: 0;
  -webkit-transition: left 150ms ease;
  transition: left 150ms ease;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab {
  top: 0;
  -webkit-transition: top 150ms ease;
  transition: top 150ms ease;
}

 .jupyter-widgets.widget-tab > .p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging {
  -webkit-transition: none;
  transition: none;
}

 /* End tabbar.css */

 :root { /* margin between inline elements */

    /* From Material Design Lite */
}

 .jupyter-widgets {
    margin: 2px;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    color: black;
    overflow: visible;
}

 .jupyter-widgets.jupyter-widgets-disconnected::before {
    line-height: 28px;
    height: 28px;
}

 .jp-Output-result > .jupyter-widgets {
    margin-left: 0;
    margin-right: 0;
}

 /* vbox and hbox */

 .widget-inline-hbox {
    /* Horizontal widgets */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
    -webkit-box-align: baseline;
        -ms-flex-align: baseline;
            align-items: baseline;
}

 .widget-inline-vbox {
    /* Vertical Widgets */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
}

 .widget-box {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    margin: 0;
    overflow: auto;
}

 .widget-gridbox {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    display: grid;
    margin: 0;
    overflow: auto;
}

 .widget-hbox {
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
        -ms-flex-direction: row;
            flex-direction: row;
}

 .widget-vbox {
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 /* General Button Styling */

 .jupyter-button {
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 0px;
    padding-bottom: 0px;
    display: inline-block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: center;
    font-size: 13px;
    cursor: pointer;

    height: 28px;
    border: 0px solid;
    line-height: 28px;
    -webkit-box-shadow: none;
            box-shadow: none;

    color: rgba(0, 0, 0, .8);
    background-color: #EEEEEE;
    border-color: #E0E0E0;
    border: none;
}

 .jupyter-button i.fa {
    margin-right: 4px;
    pointer-events: none;
}

 .jupyter-button:empty:before {
    content: "\200B"; /* zero-width space */
}

 .jupyter-widgets.jupyter-button:disabled {
    opacity: 0.6;
}

 .jupyter-button i.fa.center {
    margin-right: 0;
}

 .jupyter-button:hover:enabled, .jupyter-button:focus:enabled {
    /* MD Lite 2dp shadow */
    -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
                0 3px 1px -2px rgba(0, 0, 0, .2),
                0 1px 5px 0 rgba(0, 0, 0, .12);
            box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .14),
                0 3px 1px -2px rgba(0, 0, 0, .2),
                0 1px 5px 0 rgba(0, 0, 0, .12);
}

 .jupyter-button:active, .jupyter-button.mod-active {
    /* MD Lite 4dp shadow */
    -webkit-box-shadow: 0 4px 5px 0 rgba(0, 0, 0, .14),
                0 1px 10px 0 rgba(0, 0, 0, .12),
                0 2px 4px -1px rgba(0, 0, 0, .2);
            box-shadow: 0 4px 5px 0 rgba(0, 0, 0, .14),
                0 1px 10px 0 rgba(0, 0, 0, .12),
                0 2px 4px -1px rgba(0, 0, 0, .2);
    color: rgba(0, 0, 0, .8);
    background-color: #BDBDBD;
}

 .jupyter-button:focus:enabled {
    outline: 1px solid #64B5F6;
}

 /* Button "Primary" Styling */

 .jupyter-button.mod-primary {
    color: rgba(255, 255, 255, 1.0);
    background-color: #2196F3;
}

 .jupyter-button.mod-primary.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #1976D2;
}

 .jupyter-button.mod-primary:active {
    color: rgba(255, 255, 255, 1);
    background-color: #1976D2;
}

 /* Button "Success" Styling */

 .jupyter-button.mod-success {
    color: rgba(255, 255, 255, 1.0);
    background-color: #4CAF50;
}

 .jupyter-button.mod-success.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #388E3C;
 }

 .jupyter-button.mod-success:active {
    color: rgba(255, 255, 255, 1);
    background-color: #388E3C;
 }

 /* Button "Info" Styling */

 .jupyter-button.mod-info {
    color: rgba(255, 255, 255, 1.0);
    background-color: #00BCD4;
}

 .jupyter-button.mod-info.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #0097A7;
}

 .jupyter-button.mod-info:active {
    color: rgba(255, 255, 255, 1);
    background-color: #0097A7;
}

 /* Button "Warning" Styling */

 .jupyter-button.mod-warning {
    color: rgba(255, 255, 255, 1.0);
    background-color: #FF9800;
}

 .jupyter-button.mod-warning.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #F57C00;
}

 .jupyter-button.mod-warning:active {
    color: rgba(255, 255, 255, 1);
    background-color: #F57C00;
}

 /* Button "Danger" Styling */

 .jupyter-button.mod-danger {
    color: rgba(255, 255, 255, 1.0);
    background-color: #F44336;
}

 .jupyter-button.mod-danger.mod-active {
    color: rgba(255, 255, 255, 1);
    background-color: #D32F2F;
}

 .jupyter-button.mod-danger:active {
    color: rgba(255, 255, 255, 1);
    background-color: #D32F2F;
}

 /* Widget Button*/

 .widget-button, .widget-toggle-button {
    width: 148px;
}

 /* Widget Label Styling */

 /* Override Bootstrap label css */

 .jupyter-widgets label {
    margin-bottom: 0;
    margin-bottom: initial;
}

 .widget-label-basic {
    /* Basic Label */
    color: black;
    font-size: 13px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    line-height: 28px;
}

 .widget-label {
    /* Label */
    color: black;
    font-size: 13px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    line-height: 28px;
}

 .widget-inline-hbox .widget-label {
    /* Horizontal Widget Label */
    color: black;
    text-align: right;
    margin-right: 8px;
    width: 80px;
    -ms-flex-negative: 0;
        flex-shrink: 0;
}

 .widget-inline-vbox .widget-label {
    /* Vertical Widget Label */
    color: black;
    text-align: center;
    line-height: 28px;
}

 /* Widget Readout Styling */

 .widget-readout {
    color: black;
    font-size: 13px;
    height: 28px;
    line-height: 28px;
    overflow: hidden;
    white-space: nowrap;
    text-align: center;
}

 .widget-readout.overflow {
    /* Overflowing Readout */

    /* From Material Design Lite
        shadow-key-umbra-opacity: 0.2;
        shadow-key-penumbra-opacity: 0.14;
        shadow-ambient-shadow-opacity: 0.12;
     */
    -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .2),
                        0 3px 1px -2px rgba(0, 0, 0, .14),
                        0 1px 5px 0 rgba(0, 0, 0, .12);

    box-shadow: 0 2px 2px 0 rgba(0, 0, 0, .2),
                0 3px 1px -2px rgba(0, 0, 0, .14),
                0 1px 5px 0 rgba(0, 0, 0, .12);
}

 .widget-inline-hbox .widget-readout {
    /* Horizontal Readout */
    text-align: center;
    max-width: 148px;
    min-width: 72px;
    margin-left: 4px;
}

 .widget-inline-vbox .widget-readout {
    /* Vertical Readout */
    margin-top: 4px;
    /* as wide as the widget */
    width: inherit;
}

 /* Widget Checkbox Styling */

 .widget-checkbox {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-checkbox input[type="checkbox"] {
    margin: 0px 8px 0px 0px;
    line-height: 28px;
    font-size: large;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 0;
        flex-shrink: 0;
    -ms-flex-item-align: center;
        align-self: center;
}

 /* Widget Valid Styling */

 .widget-valid {
    height: 28px;
    line-height: 28px;
    width: 148px;
    font-size: 13px;
}

 .widget-valid i:before {
    line-height: 28px;
    margin-right: 4px;
    margin-left: 4px;

    /* from the fa class in FontAwesome: https://github.com/FortAwesome/Font-Awesome/blob/49100c7c3a7b58d50baa71efef11af41a66b03d3/css/font-awesome.css#L14 */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

 .widget-valid.mod-valid i:before {
    content: "\F00C";
    color: green;
}

 .widget-valid.mod-invalid i:before {
    content: "\F00D";
    color: red;
}

 .widget-valid.mod-valid .widget-valid-readout {
    display: none;
}

 /* Widget Text and TextArea Stying */

 .widget-textarea, .widget-text {
    width: 300px;
}

 .widget-text input[type="text"], .widget-text input[type="number"]{
    height: 28px;
    line-height: 28px;
}

 .widget-text input[type="text"]:disabled, .widget-text input[type="number"]:disabled, .widget-textarea textarea:disabled {
    opacity: 0.6;
}

 .widget-text input[type="text"], .widget-text input[type="number"], .widget-textarea textarea {
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    padding: 4px 8px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -ms-flex-negative: 1;
        flex-shrink: 1;
    outline: none !important;
}

 .widget-textarea textarea {
    height: inherit;
    width: inherit;
}

 .widget-text input:focus, .widget-textarea textarea:focus {
    border-color: #64B5F6;
}

 /* Widget Slider */

 .widget-slider .ui-slider {
    /* Slider Track */
    border: 1px solid #BDBDBD;
    background: #BDBDBD;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    position: relative;
    border-radius: 0px;
}

 .widget-slider .ui-slider .ui-slider-handle {
    /* Slider Handle */
    outline: none !important; /* focused slider handles are colored - see below */
    position: absolute;
    background-color: white;
    border: 1px solid #9E9E9E;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    z-index: 1;
    background-image: none; /* Override jquery-ui */
}

 /* Override jquery-ui */

 .widget-slider .ui-slider .ui-slider-handle:hover, .widget-slider .ui-slider .ui-slider-handle:focus {
    background-color: #2196F3;
    border: 1px solid #2196F3;
}

 .widget-slider .ui-slider .ui-slider-handle:active {
    background-color: #2196F3;
    border-color: #2196F3;
    z-index: 2;
    -webkit-transform: scale(1.2);
            transform: scale(1.2);
}

 .widget-slider  .ui-slider .ui-slider-range {
    /* Interval between the two specified value of a double slider */
    position: absolute;
    background: #2196F3;
    z-index: 0;
}

 /* Shapes of Slider Handles */

 .widget-hslider .ui-slider .ui-slider-handle {
    width: 16px;
    height: 16px;
    margin-top: -7px;
    margin-left: -7px;
    border-radius: 50%;
    top: 0;
}

 .widget-vslider .ui-slider .ui-slider-handle {
    width: 16px;
    height: 16px;
    margin-bottom: -7px;
    margin-left: -7px;
    border-radius: 50%;
    left: 0;
}

 .widget-hslider .ui-slider .ui-slider-range {
    height: 8px;
    margin-top: -3px;
}

 .widget-vslider .ui-slider .ui-slider-range {
    width: 8px;
    margin-left: -3px;
}

 /* Horizontal Slider */

 .widget-hslider {
    width: 300px;
    height: 28px;
    line-height: 28px;

    /* Override the align-items baseline. This way, the description and readout
    still seem to align their baseline properly, and we don't have to have
    align-self: stretch in the .slider-container. */
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
}

 .widgets-slider .slider-container {
    overflow: visible;
}

 .widget-hslider .slider-container {
    height: 28px;
    margin-left: 6px;
    margin-right: 6px;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
}

 .widget-hslider .ui-slider {
    /* Inner, invisible slide div */
    height: 4px;
    margin-top: 12px;
    width: 100%;
}

 /* Vertical Slider */

 .widget-vbox .widget-label {
    height: 28px;
    line-height: 28px;
}

 .widget-vslider {
    /* Vertical Slider */
    height: 200px;
    width: 72px;
}

 .widget-vslider .slider-container {
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 6px;
    margin-top: 6px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 .widget-vslider .ui-slider-vertical {
    /* Inner, invisible slide div */
    width: 4px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-left: auto;
    margin-right: auto;
}

 /* Widget Progress Styling */

 .progress-bar {
    -webkit-transition: none;
    transition: none;
}

 .progress-bar {
    height: 28px;
}

 .progress-bar {
    background-color: #2196F3;
}

 .progress-bar-success {
    background-color: #4CAF50;
}

 .progress-bar-info {
    background-color: #00BCD4;
}

 .progress-bar-warning {
    background-color: #FF9800;
}

 .progress-bar-danger {
    background-color: #F44336;
}

 .progress {
    background-color: #EEEEEE;
    border: none;
    -webkit-box-shadow: none;
            box-shadow: none;
}

 /* Horisontal Progress */

 .widget-hprogress {
    /* Progress Bar */
    height: 28px;
    line-height: 28px;
    width: 300px;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;

}

 .widget-hprogress .progress {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-top: 4px;
    margin-bottom: 4px;
    -ms-flex-item-align: stretch;
        align-self: stretch;
    /* Override bootstrap style */
    height: auto;
    height: initial;
}

 /* Vertical Progress */

 .widget-vprogress {
    height: 200px;
    width: 72px;
}

 .widget-vprogress .progress {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    width: 20px;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 0;
}

 /* Select Widget Styling */

 .widget-dropdown {
    height: 28px;
    width: 300px;
    line-height: 28px;
}

 .widget-dropdown > select {
    padding-right: 20px;
    border: 1px solid #9E9E9E;
    border-radius: 0;
    height: inherit;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    outline: none !important;
    -webkit-box-shadow: none;
            box-shadow: none;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    vertical-align: top;
    padding-left: 8px;
	appearance: none;
	-webkit-appearance: none;
	-moz-appearance: none;
    background-repeat: no-repeat;
	background-size: 20px;
	background-position: right center;
    background-image: url("data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDE5LjIuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IgoJIHZpZXdCb3g9IjAgMCAxOCAxOCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMTggMTg7IiB4bWw6c3BhY2U9InByZXNlcnZlIj4KPHN0eWxlIHR5cGU9InRleHQvY3NzIj4KCS5zdDB7ZmlsbDpub25lO30KPC9zdHlsZT4KPHBhdGggZD0iTTUuMiw1LjlMOSw5LjdsMy44LTMuOGwxLjIsMS4ybC00LjksNWwtNC45LTVMNS4yLDUuOXoiLz4KPHBhdGggY2xhc3M9InN0MCIgZD0iTTAtMC42aDE4djE4SDBWLTAuNnoiLz4KPC9zdmc+Cg");
}

 .widget-dropdown > select:focus {
    border-color: #64B5F6;
}

 .widget-dropdown > select:disabled {
    opacity: 0.6;
}

 /* To disable the dotted border in Firefox around select controls.
   See http://stackoverflow.com/a/18853002 */

 .widget-dropdown > select:-moz-focusring {
    color: transparent;
    text-shadow: 0 0 0 #000;
}

 /* Select and SelectMultiple */

 .widget-select {
    width: 300px;
    line-height: 28px;

    /* Because Firefox defines the baseline of a select as the bottom of the
    control, we align the entire control to the top and add padding to the
    select to get an approximate first line baseline alignment. */
    -webkit-box-align: start;
        -ms-flex-align: start;
            align-items: flex-start;
}

 .widget-select > select {
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    -webkit-box-flex: 1;
        -ms-flex: 1 1 148px;
            flex: 1 1 148px;
    outline: none !important;
    overflow: auto;
    height: inherit;

    /* Because Firefox defines the baseline of a select as the bottom of the
    control, we align the entire control to the top and add padding to the
    select to get an approximate first line baseline alignment. */
    padding-top: 5px;
}

 .widget-select > select:focus {
    border-color: #64B5F6;
}

 .wiget-select > select > option {
    padding-left: 4px;
    line-height: 28px;
    /* line-height doesn't work on some browsers for select options */
    padding-top: calc(28px - var(--jp-widgets-font-size) / 2);
    padding-bottom: calc(28px - var(--jp-widgets-font-size) / 2);
}

 /* Toggle Buttons Styling */

 .widget-toggle-buttons {
    line-height: 28px;
}

 .widget-toggle-buttons .widget-toggle-button {
    margin-left: 2px;
    margin-right: 2px;
}

 .widget-toggle-buttons .jupyter-button:disabled {
    opacity: 0.6;
}

 /* Radio Buttons Styling */

 .widget-radio {
    width: 300px;
    line-height: 28px;
}

 .widget-radio-box {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    margin-bottom: 8px;
}

 .widget-radio-box label {
    height: 20px;
    line-height: 20px;
    font-size: 13px;
}

 .widget-radio-box input {
    height: 20px;
    line-height: 20px;
    margin: 0 8px 0 1px;
    float: left;
}

 /* Color Picker Styling */

 .widget-colorpicker {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-colorpicker > .widget-colorpicker-input {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    min-width: 72px;
}

 .widget-colorpicker input[type="color"] {
    width: 28px;
    height: 28px;
    padding: 0 2px; /* make the color square actually square on Chrome on OS X */
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    border-left: none;
    -webkit-box-flex: 0;
        -ms-flex-positive: 0;
            flex-grow: 0;
    -ms-flex-negative: 0;
        flex-shrink: 0;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    -ms-flex-item-align: stretch;
        align-self: stretch;
    outline: none !important;
}

 .widget-colorpicker.concise input[type="color"] {
    border-left: 1px solid #9E9E9E;
}

 .widget-colorpicker input[type="color"]:focus, .widget-colorpicker input[type="text"]:focus {
    border-color: #64B5F6;
}

 .widget-colorpicker input[type="text"] {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    outline: none !important;
    height: 28px;
    line-height: 28px;
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    font-size: 13px;
    padding: 4px 8px;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    -ms-flex-negative: 1;
        flex-shrink: 1;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
}

 .widget-colorpicker input[type="text"]:disabled {
    opacity: 0.6;
}

 /* Date Picker Styling */

 .widget-datepicker {
    width: 300px;
    height: 28px;
    line-height: 28px;
}

 .widget-datepicker input[type="date"] {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    min-width: 0; /* This makes it possible for the flexbox to shrink this input */
    outline: none !important;
    height: 28px;
    border: 1px solid #9E9E9E;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    font-size: 13px;
    padding: 4px 8px;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
}

 .widget-datepicker input[type="date"]:focus {
    border-color: #64B5F6;
}

 .widget-datepicker input[type="date"]:invalid {
    border-color: #FF9800;
}

 .widget-datepicker input[type="date"]:disabled {
    opacity: 0.6;
}

 /* Play Widget */

 .widget-play {
    width: 148px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .widget-play .jupyter-button {
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    height: auto;
}

 .widget-play .jupyter-button:disabled {
    opacity: 0.6;
}

 /* Tab Widget */

 .jupyter-widgets.widget-tab {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
}

 .jupyter-widgets.widget-tab > .p-TabBar {
    /* Necessary so that a tab can be shifted down to overlay the border of the box below. */
    overflow-x: visible;
    overflow-y: visible;
}

 .jupyter-widgets.widget-tab > .p-TabBar > .p-TabBar-content {
    /* Make sure that the tab grows from bottom up */
    -webkit-box-align: end;
        -ms-flex-align: end;
            align-items: flex-end;
    min-width: 0;
    min-height: 0;
}

 .jupyter-widgets.widget-tab > .widget-tab-contents {
    width: 100%;
    -webkit-box-sizing: border-box;
            box-sizing: border-box;
    margin: 0;
    background: white;
    color: rgba(0, 0, 0, .8);
    border: 1px solid #9E9E9E;
    padding: 15px;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    overflow: auto;
}

 .jupyter-widgets.widget-tab > .p-TabBar {
    font: 13px Helvetica, Arial, sans-serif;
    min-height: 25px;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab {
    -webkit-box-flex: 0;
        -ms-flex: 0 1 144px;
            flex: 0 1 144px;
    min-width: 35px;
    min-height: 25px;
    line-height: 24px;
    margin-left: -1px;
    padding: 0px 10px;
    background: #EEEEEE;
    color: rgba(0, 0, 0, .5);
    border: 1px solid #9E9E9E;
    border-bottom: none;
    position: relative;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-current {
    color: rgba(0, 0, 0, 1.0);
    /* We want the background to match the tab content background */
    background: white;
    min-height: 26px;
    -webkit-transform: translateY(1px);
            transform: translateY(1px);
    overflow: visible;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab.p-mod-current:before {
    position: absolute;
    top: -1px;
    left: -1px;
    content: '';
    height: 2px;
    width: calc(100% + 2px);
    background: #2196F3;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab:first-child {
    margin-left: 0;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tab:hover:not(.p-mod-current) {
    background: white;
    color: rgba(0, 0, 0, .8);
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-mod-closable > .p-TabBar-tabCloseIcon {
    margin-left: 4px;
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-mod-closable > .p-TabBar-tabCloseIcon:before {
    font-family: FontAwesome;
    content: '\F00D'; /* close */
}

 .jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabIcon,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabLabel,
.jupyter-widgets.widget-tab > .p-TabBar .p-TabBar-tabCloseIcon {
    line-height: 24px;
}

 /* Accordion Widget */

 .p-Collapse {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .p-Collapse-header {
    padding: 4px;
    cursor: pointer;
    color: rgba(0, 0, 0, .5);
    background-color: #EEEEEE;
    border: 1px solid #9E9E9E;
    padding: 10px 15px;
    font-weight: bold;
}

 .p-Collapse-header:hover {
    background-color: white;
    color: rgba(0, 0, 0, .8);
}

 .p-Collapse-open > .p-Collapse-header {
    background-color: white;
    color: rgba(0, 0, 0, 1.0);
    cursor: default;
    border-bottom: none;
}

 .p-Collapse .p-Collapse-header::before {
    content: '\F0DA\A0';  /* caret-right, non-breaking space */
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

 .p-Collapse-open > .p-Collapse-header::before {
    content: '\F0D7\A0'; /* caret-down, non-breaking space */
}

 .p-Collapse-contents {
    padding: 15px;
    background-color: white;
    color: rgba(0, 0, 0, .8);
    border-left: 1px solid #9E9E9E;
    border-right: 1px solid #9E9E9E;
    border-bottom: 1px solid #9E9E9E;
    overflow: auto;
}

 .p-Accordion {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: stretch;
        -ms-flex-align: stretch;
            align-items: stretch;
}

 .p-Accordion .p-Collapse {
    margin-bottom: 0;
}

 .p-Accordion .p-Collapse + .p-Collapse {
    margin-top: 4px;
}

 /* HTML widget */

 .widget-html, .widget-htmlmath {
    font-size: 13px;
}

 .widget-html > .widget-html-content, .widget-htmlmath > .widget-html-content {
    /* Fill out the area in the HTML widget */
    -ms-flex-item-align: stretch;
        align-self: stretch;
    -webkit-box-flex: 1;
        -ms-flex-positive: 1;
            flex-grow: 1;
    -ms-flex-negative: 1;
        flex-shrink: 1;
    /* Makes sure the baseline is still aligned with other elements */
    line-height: 28px;
    /* Make it possible to have absolutely-positioned elements in the html */
    position: relative;
}
</style><link id="favicon" type="image/x-icon" rel="shortcut icon" href="http://localhost:8888/static/base/images/favicon-notebook.ico"><style type="text/css">@font-face {font-family: STIXMathJax_Main-italic; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/woff/STIXMathJax_Main-Italic.woff?V=2.7.4') format('woff'), url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/otf/STIXMathJax_Main-Italic.otf?V=2.7.4') format('opentype')}
</style><style type="text/css">@font-face {font-family: STIXMathJax_Main; src: url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/woff/STIXMathJax_Main-Regular.woff?V=2.7.4') format('woff'), url('http://localhost:8888/static/components/MathJax/fonts/HTML-CSS/STIX-Web/otf/STIXMathJax_Main-Regular.otf?V=2.7.4') format('opentype')}
</style></head>

<body class="notebook_app command_mode" data-jupyter-api-token="b07d09b1f3066b14e76bf348e3dc901d2d5bf73a2ec5334f" data-base-url="/" data-ws-url="" data-notebook-name="Untitled1.ipynb" data-notebook-path="Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Untitled1.ipynb" dir="ltr" style=""><div style="visibility: hidden; overflow: hidden; position: absolute; top: 0px; height: 1px; width: auto; padding: 0px; border: 0px; margin: 0px; text-align: left; text-indent: 0px; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal;"><div id="MathJax_Hidden"><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br></div></div><div id="MathJax_Message" style="display: none;"></div>

<noscript>
    <div id='noscript'>
      Jupyter Notebook requires JavaScript.<br>
      Please enable it to proceed. 
  </div>
</noscript>

<div id="header" style="display: block;">
  <div id="header-container" class="container">
  <div id="ipython_notebook" class="nav navbar-brand"><a href="http://localhost:8888/tree?token=b07d09b1f3066b14e76bf348e3dc901d2d5bf73a2ec5334f" title="dashboard">
      <img src="./README_files/logo.png" alt="Jupyter Notebook">
  </a></div>

  


<span id="save_widget" class="save_widget">
    <span id="notebook_name" class="filename">Varieties_of_the_wheat_seed_dataset</span>
    <span class="checkpoint_status" title="mer. 27 févr. 2019 09:25">Last Checkpoint: il y a une heure</span>
    <span class="autosave_status">(autosaved)</span>
<i id="notebook-trusted-indicator" class="fa notebook-trusted fa-check" title="Notebook is trusted"></i></span>

<span id="kernel_logo_widget">
  
  <img class="current_kernel_logo" alt="Current Kernel Logo" src="./README_files/logo-64x64.png" title="Python 3" style="display: inline;">
  
</span>


  
  
  
  

    <span id="login_widget">
      
        <button id="logout" class="btn btn-sm navbar-btn">Logout</button>
      
    </span>

  

  
  
  </div>
  <div class="header-bar"></div>

  
<div id="menubar-container" class="container">
<div id="menubar">
    <div id="menus" class="navbar navbar-default" role="navigation">
        <div class="container-fluid">
            <button type="button" class="btn btn-default navbar-btn navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
              <i class="fa fa-bars"></i>
              <span class="navbar-text">Menu</span>
            </button>
            <p id="kernel_indicator" class="navbar-text indicator_area">
              <span class="kernel_indicator_name">Python 3</span>
              <i id="kernel_indicator_icon" class="kernel_idle_icon" title="Kernel Idle"></i>
            </p>
            <i id="readonly-indicator" class="navbar-text" title="This notebook is read-only" style="display: none;">
                <span class="fa-stack">
                    <i class="fa fa-save fa-stack-1x"></i>
                    <i class="fa fa-ban fa-stack-2x text-danger"></i>
                </span>
            </i>
            <i id="modal_indicator" class="navbar-text modal_indicator" title="Command Mode"></i>
            <span id="notification_area"><div id="notification_kernel" class="notification_widget btn btn-xs navbar-btn undefined info" style="display: none;"><span></span></div><div id="notification_notebook" class="notification_widget btn btn-xs navbar-btn" style="display: none;"><span></span></div><div id="notification_trusted" class="notification_widget btn btn-xs navbar-btn" disabled="disabled" style="cursor: help;"><span title="Javascript enabled for notebook display">Trusted</span></div><div id="notification_widgets" class="notification_widget btn btn-xs navbar-btn" style="display: none;"><span></span></div></span>
            <div class="navbar-collapse collapse">
              <ul class="nav navbar-nav">
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="dropdown-toggle" data-toggle="dropdown">File</a>
                    <ul id="file_menu" class="dropdown-menu">
                        <li id="new_notebook" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">New Notebook</a>
                            <ul class="dropdown-menu" id="menu-new-notebook-submenu"><li id="new-notebook-submenu-python3"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Python 3</a></li></ul>
                        </li>
                        <li id="open_notebook" title="Opens a new window with the Dashboard view">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Open...</a></li>
                        <!-- <hr/> -->
                        <li class="divider"></li>
                        <li id="copy_notebook" title="Open a copy of this notebook&#39;s contents and start a new kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Make a Copy...</a></li>
                        <li id="save_notebook_as" title="Save a copy of the notebook&#39;s contents and start a new kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Save as...</a></li>
                        <li id="rename_notebook"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Rename...</a></li>
                        <li id="save_checkpoint"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Save and Checkpoint</a></li>
                        <!-- <hr/> -->
                        <li class="divider"></li>
                        <li id="restore_checkpoint" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Revert to Checkpoint</a>
                          <ul class="dropdown-menu"><li><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">mercredi 27 février 2019 09:25</a></li></ul>
                        </li>
                        <li class="divider"></li>
                        <li id="print_preview"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Print Preview</a></li>
                        <li class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Download as</a>
                            <ul id="download_menu" class="dropdown-menu">
                                <li id="download_ipynb"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Notebook (.ipynb)</a></li>
                                <li id="download_script"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Python (.py)</a></li>
                                <li id="download_html"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">HTML (.html)</a></li>
                                <li id="download_slides"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Reveal.js slides (.html)</a></li>
                                <li id="download_markdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Markdown (.md)</a></li>
                                <li id="download_rst"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">reST (.rst)</a></li>
                                <li id="download_latex"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">LaTeX (.tex)</a></li>
                                <li id="download_pdf"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">PDF via LaTeX (.pdf)</a></li>
                                
                                <li id="download_asciidoc">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">asciidoc (.asciidoc)</a>
                                </li>
                                
                                <li id="download_custom">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.txt)</a>
                                </li>
                                
                                <li id="download_html">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_ch">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_embed">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_toc">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_html_with_toclenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.html)</a>
                                </li>
                                
                                <li id="download_latex">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">latex (.tex)</a>
                                </li>
                                
                                <li id="download_latex_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">latex (.tex)</a>
                                </li>
                                
                                <li id="download_markdown">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">markdown (.md)</a>
                                </li>
                                
                                <li id="download_notebook">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">notebook (.ipynb)</a>
                                </li>
                                
                                <li id="download_pdf">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">pdf (.tex)</a>
                                </li>
                                
                                <li id="download_python">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">python (.py)</a>
                                </li>
                                
                                <li id="download_rst">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">rst (.rst)</a>
                                </li>
                                
                                <li id="download_script">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">custom (.txt)</a>
                                </li>
                                
                                <li id="download_selectLanguage">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">notebook (.ipynb)</a>
                                </li>
                                
                                <li id="download_slides">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">slides (.slides.html)</a>
                                </li>
                                
                                <li id="download_slides_with_lenvs">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">slides (.slides.html)</a>
                                </li>
                                
                            <li id="download_html_embed"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">HTML Embedded (.html)</a></li></ul>
                        </li>
                        <li class="dropdown-submenu hidden"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Deploy as</a>
                            <ul id="deploy_menu" class="dropdown-menu"></ul>
                        </li>
                        <li class="divider"></li>
                        <li id="trust_notebook" title="Trust the output of this notebook" class="disabled">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Trusted Notebook</a></li>
                        <li class="divider"></li>
                        <li id="close_and_halt" title="Shutdown this notebook&#39;s kernel, and close this window">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Close and Halt</a></li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Edit</a>
                    <ul id="edit_menu" class="dropdown-menu">
                        <li id="cut_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Cut Cells</a></li>
                        <li id="copy_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Copy Cells</a></li>
                        <li id="paste_cell_above" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Paste Cells Above</a></li>
                        <li id="paste_cell_below" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Paste Cells Below</a></li>
                        <li id="paste_cell_replace" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Paste Cells &amp; Replace</a></li>
                        <li id="delete_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Delete Cells</a></li>
                        <li id="undelete_cell" class=""><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Undo Delete Cells</a></li>
                        <li class="divider"></li>
                        <li id="split_cell"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Split Cell</a></li>
                        <li id="merge_cell_above"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Merge Cell Above</a></li>
                        <li id="merge_cell_below"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Merge Cell Below</a></li>
                        <li class="divider"></li>
                        <li id="move_cell_up"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Move Cell Up</a></li>
                        <li id="move_cell_down"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Move Cell Down</a></li>
                        <li class="divider"></li>
                        <li id="edit_nb_metadata"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Edit Notebook Metadata</a></li>
                        <li class="divider"></li>
                        <li id="find_and_replace"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#"> Find and Replace </a></li>
                        <li class="divider"></li>
                        <li id="cut_cell_attachments"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Cut Cell Attachments</a></li>
                        <li id="copy_cell_attachments"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Copy Cell Attachments</a></li>
                        <li id="paste_cell_attachments" class="disabled"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Paste Cell Attachments</a></li>
                        <li class="divider"></li>
                        <li id="insert_image" class="disabled"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#"> Insert Image </a></li>
                    <li class="divider"></li><li><a target="_blank" title="Opens in a new window" href="http://localhost:8888/nbextensions/"> <i class="fa fa-cogs menu-icon pull-right"></i><span>nbextensions config</span></a></li></ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="dropdown-toggle" data-toggle="dropdown">View</a>
                    <ul id="view_menu" class="dropdown-menu">
                        <li id="toggle_header" title="Show/Hide the logo and notebook title (above menu bar)">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Toggle Header</a>
                        </li>
                        <li id="toggle_toolbar" title="Show/Hide the action icons (below menu bar)">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Toggle Toolbar</a>
                        </li>
                        <li id="toggle_line_numbers" title="Show/Hide line numbers in cells">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Toggle Line Numbers</a>
                        </li>
                        <li id="menu-cell-toolbar" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Cell Toolbar</a>
                            <ul class="dropdown-menu" id="menu-cell-toolbar-submenu"><li data-name="None"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">None</a></li><li data-name="Edit%20Metadata"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Edit Metadata</a></li><li data-name="Raw%20Cell%20Format"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Raw Cell Format</a></li><li data-name="Slideshow"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Slideshow</a></li><li data-name="Attachments"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Attachments</a></li><li data-name="Tags"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Tags</a></li></ul>
                        </li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Insert</a>
                    <ul id="insert_menu" class="dropdown-menu">
                        <li id="insert_cell_above" title="Insert an empty Code cell above the currently active cell">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Insert Cell Above</a></li>
                        <li id="insert_cell_below" title="Insert an empty Code cell below the currently active cell">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Insert Cell Below</a></li>
                    <li class="divider"></li><li><a title="Insert a heading cell above the selected cell" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Insert Heading Above</a></li><li><a title="Insert a heading cell below the selected cell&#39;s section" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Insert Heading Below</a></li></ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Cell</a>
                    <ul id="cell_menu" class="dropdown-menu">
                        <li id="run_cell" title="Run this cell, and move cursor to the next one">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Run Cells</a></li>
                        <li id="run_cell_select_below" title="Run this cell, select below">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Run Cells and Select Below</a></li>
                        <li id="run_cell_insert_below" title="Run this cell, insert below">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Run Cells and Insert Below</a></li>
                        <li id="run_all_cells" title="Run all cells in the notebook">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Run All</a></li>
                        <li id="run_all_cells_above" title="Run all cells above (but not including) this cell">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Run All Above</a></li>
                        <li id="run_all_cells_below" title="Run this cell and all cells below it">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Run All Below</a></li>
                        <li class="divider"></li>
                        <li id="change_cell_type" class="dropdown-submenu" title="All cells in the notebook have a cell type. By default, new cells are created as &#39;Code&#39; cells">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Cell Type</a>
                            <ul class="dropdown-menu">
                              <li id="to_code" title="Contents will be sent to the kernel for execution, and output will display in the footer of cell">
                                  <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Code</a></li>
                              <li id="to_markdown" title="Contents will be rendered as HTML and serve as explanatory text">
                                  <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Markdown</a></li>
                              <li id="to_raw" title="Contents will pass through nbconvert unmodified">
                                  <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Raw NBConvert</a></li>
                            </ul>
                        </li>
                        <li class="divider"></li>
                        <li id="current_outputs" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Current Outputs</a>
                            <ul class="dropdown-menu">
                                <li id="toggle_current_output" title="Hide/Show the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Toggle</a>
                                </li>
                                <li id="toggle_current_output_scroll" title="Scroll the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Toggle Scrolling</a>
                                </li>
                                <li id="clear_current_output" title="Clear the output of the current cell">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Clear</a>
                                </li>
                            </ul>
                        </li>
                        <li id="all_outputs" class="dropdown-submenu"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">All Output</a>
                            <ul class="dropdown-menu">
                                <li id="toggle_all_output" title="Hide/Show the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Toggle</a>
                                </li>
                                <li id="toggle_all_output_scroll" title="Scroll the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Toggle Scrolling</a>
                                </li>
                                <li id="clear_all_output" title="Clear the output of all cells">
                                    <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Clear</a>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Kernel</a>
                    <ul id="kernel_menu" class="dropdown-menu">
                        <li id="int_kernel" title="Send Keyboard Interrupt (CTRL-C) to the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Interrupt</a>
                        </li>
                        <li id="restart_kernel" title="Restart the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Restart</a>
                        </li>
                        <li id="restart_clear_output" title="Restart the Kernel and clear all output">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Restart &amp; Clear Output</a>
                        </li>
                        <li id="restart_run_all" title="Restart the Kernel and re-run the notebook">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Restart &amp; Run All</a>
                        </li>
                        <li id="reconnect_kernel" title="Reconnect to the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Reconnect</a>
                        </li>
                        <li id="shutdown_kernel" title="Shutdown the Kernel">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Shutdown</a>
                        </li>
                        <li class="divider"></li>
                        <li id="menu-change-kernel" class="dropdown-submenu">
                            <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Change kernel</a>
                            <ul class="dropdown-menu" id="menu-change-kernel-submenu"><li id="kernel-submenu-python3"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Python 3</a></li></ul>
                        </li>
                    </ul>
                </li><li id="Navigate" class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" id="Navigate_sub" class="dropdown-toggle" data-toggle="dropdown">Navigate</a><ul id="Navigate_menu" class="dropdown-menu ui-resizable" style=""><div id="navigate_menu" class="toc" style="width: 160px; height: 0px;"><ul class="toc-item"><li><span><i class="fa fa-fw fa-caret-down"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Project-Overview" data-toc-modified-id="Project-Overview-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>Project Overview</a></span><ul class="toc-item"><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Varieties-of-the-wheat-seed-dataset" data-toc-modified-id="Varieties-of-the-wheat-seed-dataset-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>Varieties of the wheat seed dataset</a></span></li><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Exploratory-Data-Analysis" data-toc-modified-id="Exploratory-Data-Analysis-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>Exploratory Data Analysis</a></span></li><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#KMEANS-CLUSTERING" data-toc-modified-id="KMEANS-CLUSTERING-1.3"><span class="toc-item-num">1.3&nbsp;&nbsp;</span>KMEANS CLUSTERING</a></span></li><li><span><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Elbow-point" data-toc-modified-id="Elbow-point-1.4" class="toc-item-highlight-select"><span class="toc-item-num">1.4&nbsp;&nbsp;</span>Elbow point</a></span></li></ul></li></ul></div><div class="ui-resizable-handle ui-resizable-e" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div></ul></li>
                <li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" data-toggle="dropdown" class="dropdown-toggle">Widgets</a><ul id="widget-submenu" class="dropdown-menu"><li title="Save the notebook with the widget state information for static rendering"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Save Notebook Widget State</a></li><li title="Clear the widget state information from the notebook"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Clear Notebook Widget State</a></li><ul class="divider"></ul><li title="Download the widget state as a JSON file"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Download Widget State</a></li><li title="Embed interactive widgets"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Embed Widgets</a></li></ul></li><li class="dropdown"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="dropdown-toggle" data-toggle="dropdown">Help</a>
                    <ul id="help_menu" class="dropdown-menu">
                        
                        <li id="notebook_tour" title="A quick tour of the notebook user interface"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">User Interface Tour</a></li>
                        <li id="keyboard_shortcuts" title="Opens a tooltip with all keyboard shortcuts"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Keyboard Shortcuts</a></li>
                        <li id="edit_keyboard_shortcuts" title="Opens a dialog allowing you to edit Keyboard shortcuts"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">Edit Keyboard Shortcuts</a></li>
                        <li class="divider"></li>
                        

						
                        
                            
                                <li><a rel="noreferrer" href="http://nbviewer.jupyter.org/github/ipython/ipython/blob/3.x/examples/Notebook/Index.ipynb" target="_blank" title="Opens in a new window">
                                
                                    <i class="fa fa-external-link menu-icon pull-right"></i>
                                

                                Notebook Help
                                </a></li>
                            
                                <li><a rel="noreferrer" href="https://help.github.com/articles/markdown-basics/" target="_blank" title="Opens in a new window">
                                
                                    <i class="fa fa-external-link menu-icon pull-right"></i>
                                

                                Markdown
                                </a></li>
                            
                            
                        
                        <li><a title="Jupyter_contrib_nbextensions documentation" id="jupyter_contrib_nbextensions_help" href="http://jupyter-contrib-nbextensions.readthedocs.io/en/latest/" target="_blank">Jupyter-contrib <br> nbextensions<i class="fa fa-external-link menu-icon pull-right"></i></a></li><li id="kernel-help-links" class="divider"></li><li><a target="_blank" title="Opens in a new window" href="https://docs.python.org/3.7?v=20190227082127"><i class="fa fa-external-link menu-icon pull-right"></i><span>Python Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://ipython.org/documentation.html?v=20190227082127"><i class="fa fa-external-link menu-icon pull-right"></i><span>IPython Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://docs.scipy.org/doc/numpy/reference/?v=20190227082127"><i class="fa fa-external-link menu-icon pull-right"></i><span>NumPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://docs.scipy.org/doc/scipy/reference/?v=20190227082127"><i class="fa fa-external-link menu-icon pull-right"></i><span>SciPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://matplotlib.org/contents.html?v=20190227082127"><i class="fa fa-external-link menu-icon pull-right"></i><span>Matplotlib Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="http://docs.sympy.org/latest/index.html?v=20190227082127"><i class="fa fa-external-link menu-icon pull-right"></i><span>SymPy Reference</span></a></li><li><a target="_blank" title="Opens in a new window" href="https://pandas.pydata.org/pandas-docs/stable/?v=20190227082127"><i class="fa fa-external-link menu-icon pull-right"></i><span>pandas Reference</span></a></li><li class="divider"></li>
                        <li title="About Jupyter Notebook"><a id="notebook_about" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#">About</a></li>
                        
                    </ul>
                </li>
              </ul>
            </div>
        </div>
    </div>
</div>

<div id="maintoolbar" class="navbar">
  <div class="toolbar-inner navbar-inner navbar-nobg">
    <div id="maintoolbar-container" class="container toolbar"><div class="btn-group" id="save-notbook"><button class="btn btn-default" title="Save and Checkpoint" data-jupyter-action="jupyter-notebook:save-notebook"><i class="fa-save fa"></i></button></div><div class="btn-group" id="insert_above_below"><button class="btn btn-default" title="insert cell below" data-jupyter-action="jupyter-notebook:insert-cell-below"><i class="fa-plus fa"></i></button></div><div class="btn-group" id="cut_copy_paste"><button class="btn btn-default" title="cut selected cells" data-jupyter-action="jupyter-notebook:cut-cell"><i class="fa-cut fa"></i></button><button class="btn btn-default" title="copy selected cells" data-jupyter-action="jupyter-notebook:copy-cell"><i class="fa-copy fa"></i></button><button class="btn btn-default" title="paste cells below" data-jupyter-action="jupyter-notebook:paste-cell-below"><i class="fa-paste fa"></i></button></div><div class="btn-group" id="move_up_down"><button class="btn btn-default" title="move selected cells up" data-jupyter-action="jupyter-notebook:move-cell-up"><i class="fa-arrow-up fa"></i></button><button class="btn btn-default" title="move selected cells down" data-jupyter-action="jupyter-notebook:move-cell-down"><i class="fa-arrow-down fa"></i></button></div><div class="btn-group" id="run_int"><button class="btn btn-default" title="Run" data-jupyter-action="jupyter-notebook:run-cell-and-select-next"><i class="fa-step-forward fa"></i><span class="toolbar-btn-label">Run</span></button><button class="btn btn-default" title="interrupt the kernel" data-jupyter-action="jupyter-notebook:interrupt-kernel"><i class="fa-stop fa"></i></button><button class="btn btn-default" title="restart the kernel (with dialog)" data-jupyter-action="jupyter-notebook:confirm-restart-kernel"><i class="fa-repeat fa"></i></button><button class="btn btn-default" title="restart the kernel, then re-run the whole notebook (with dialog)" data-jupyter-action="jupyter-notebook:confirm-restart-kernel-and-run-all-cells"><i class="fa-forward fa"></i></button></div><select id="cell_type" class="form-control select-xs"><option value="code">Code</option><option value="markdown">Markdown</option><option value="raw">Raw NBConvert</option><option value="heading">Heading</option><option value="multiselect" disabled="disabled" style="display: none;">-</option></select><div class="btn-group"><button class="btn btn-default" title="open the command palette" data-jupyter-action="jupyter-notebook:show-command-palette"><i class="fa-keyboard-o fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Variable Inspector" data-jupyter-action="varInspector:toggle-variable-inspector" id="varInspector_button"><i class="fa-crosshairs fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Increase code font size" data-jupyter-action="code_font_size:increase-code-font-size"><i class="fa-search-plus fa"></i></button><button class="btn btn-default" title="Decrease code font size" data-jupyter-action="code_font_size:decrease-code-font-size"><i class="fa-search-minus fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Create/Edit Gist of Notebook" data-jupyter-action="gist_it:create-gist-from-notebook"><i class="fa-github fa"></i></button></div><div class="btn-group" id="code_prettify_button"><button class="btn btn-default" title="code_prettify selected cell(s) (add shift for all cells)"><i class="fa-legal fa"></i></button></div><div class="btn-group" id="autopep8_button"><button class="btn btn-default" title="autopep8 selected cell(s) (add shift for all cells)"><i class="fa-legal fa"></i></button></div><div class="btn-group"><button class="btn btn-default" title="Table of Contents" data-jupyter-action="toc2:toggle-toc" id="toc_button"><i class="fa-list fa"></i></button></div></div>
  </div>
</div>
</div>

<div class="lower-header-bar"></div>

</div>

<div id="site" style="display: block; height: 595.444px;"><div id="toc-wrapper" class="ui-draggable ui-resizable sidebar-wrapper" style="display: none; position: relative; width: 20%; top: 163.333px; left: 0px;"><div id="toc-header"><span class="header">Contents </span><i class="fa fa-fw hide-btn" title="Hide ToC"></i><i class="fa fa-fw fa-refresh" title="Reload ToC"></i><i class="fa fa-fw fa-cog" title="ToC settings"></i></div><div id="toc" class="toc"><ul class="toc-item"><li><span class="highlight_on_scroll"><i class="fa fa-fw fa-caret-down"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Project-Overview" data-toc-modified-id="Project-Overview-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>Project Overview</a></span><ul class="toc-item"><li><span class=""><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Varieties-of-the-wheat-seed-dataset" data-toc-modified-id="Varieties-of-the-wheat-seed-dataset-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>Varieties of the wheat seed dataset</a></span></li><li><span class=""><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Exploratory-Data-Analysis" data-toc-modified-id="Exploratory-Data-Analysis-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>Exploratory Data Analysis</a></span></li><li><span class=""><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#KMEANS-CLUSTERING" data-toc-modified-id="KMEANS-CLUSTERING-1.3"><span class="toc-item-num">1.3&nbsp;&nbsp;</span>KMEANS CLUSTERING</a></span></li><li><span class=""><i class="fa fa-fw"></i><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Elbow-point" data-toc-modified-id="Elbow-point-1.4" class="toc-item-highlight-select"><span class="toc-item-num">1.4&nbsp;&nbsp;</span>Elbow point</a></span></li></ul></li></ul></div><div class="ui-resizable-handle ui-resizable-n" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-e ui-icon ui-icon-grip-dotted-vertical" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-w" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-sw" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-ne" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-nw" style="z-index: 90;"></div></div>


<div id="ipython-main-app">
    <div id="notebook_panel">
        <div id="notebook" tabindex="-1"><div class="container" id="notebook-container"><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h1"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 5.33334px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 33px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.33334px; top: 0px; height: 21.3333px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-1"># Project Overview</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 33px;"></div><div class="CodeMirror-gutters" style="display: none; height: 44px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h1 id="Project-Overview" data-toc-modified-id="Project-Overview-1"><a class="toc-mod-link" id="Project-Overview-1"></a><span class="toc-item-num">1&nbsp;&nbsp;</span>Project Overview<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Project-Overview">¶</a></h1>
</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 105.778px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 79px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 105.778px; top: 0px; height: 16.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">This dataset provides measurements of the geometrical properties of kernels belonging to three different varieties of the wheat. A soft X-ray technique and GRAINS package were used to construct all seven, real-valued attributes. Original dataset is available at UCI Machine Learning Repository Seed dataset.</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 79px;"></div><div class="CodeMirror-gutters" style="display: none; height: 90px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p>This dataset provides measurements of the geometrical properties of kernels belonging to three different varieties of the wheat. A soft X-ray technique and GRAINS package were used to construct all seven, real-valued attributes. Original dataset is available at UCI Machine Learning Repository Seed dataset.</p>
</div></div></div><div class="cell text_cell unrendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; padding-right: 0px; padding-bottom: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 282px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 16.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">The file is processed for columns names, separators (longer than 1 characters and also of different form), while reading. The datafile contain following 7 features and 1 target class.</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">Features are:</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">A: Area</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">P: Perimeter</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">C: Compactness {C = 4piA/P^2}</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">LK: Length of Kernel</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">WK: Width of Kernel</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">A_Coef: Asymmetry Coefficient</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">LKG: Length of Kernel Groove</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">Target Class is:</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">target: target class (0, 1, 2)</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 282px;"></div><div class="CodeMirror-gutters" style="display: none; height: 293px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"></div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 38.9305px; left: 259.556px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 62px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 259.556px; top: 33.3333px; height: 17.3334px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"> this is unsupervised learning project, the target class is not available in such learning. we can ignore the target class or use it for just to re-check what the algorithm is clustering.</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 62px;"></div><div class="CodeMirror-gutters" style="display: none; height: 73px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p> this is unsupervised learning project, the target class is not available in such learning. we can ignore the target class or use it for just to re-check what the algorithm is clustering.</p>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h2"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 32px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 20.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-2">## Varieties of the wheat seed dataset</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 32px;"></div><div class="CodeMirror-gutters" style="display: none; height: 43px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h2 id="Varieties-of-the-wheat-seed-dataset" data-toc-modified-id="Varieties-of-the-wheat-seed-dataset-1.1"><a class="toc-mod-link" id="Varieties-of-the-wheat-seed-dataset-1.1"></a><span class="toc-item-num">1.1&nbsp;&nbsp;</span>Varieties of the wheat seed dataset<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Varieties-of-the-wheat-seed-dataset">¶</a></h2>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 351.056px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 351.056px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### The required llibrairies are imported as below</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="The-required-llibrairies-are-imported-as-below">The required llibrairies are imported as below<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#The-required-llibrairies-are-imported-as-below">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[1]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 90.0417px; left: 157px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 247.181px; margin-bottom: -19px; border-right-width: 11px; min-height: 113px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 144px; top: 84.4444px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">pandas</span> <span class="cm-keyword">as</span> <span class="cm-variable">pd</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">numpy</span> <span class="cm-keyword">as</span> <span class="cm-variable">np</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">matplotlib</span>.<span class="cm-property">pyplot</span> <span class="cm-keyword">as</span> <span class="cm-variable">plt</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">import</span> <span class="cm-variable">seaborn</span> <span class="cm-keyword">as</span> <span class="cm-variable">sns</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">sns</span>.<span class="cm-property">set_style</span>(<span class="cm-string">'whitegrid'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-operator">%</span><span class="cm-variable">matplotlib</span> <span class="cm-variable">inline</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 113px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 124px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's read the datafile Seed_Data.csv and show the head of the file</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-read-the-datafile-Seed_Data.csv-and-show-the-head-of-the-file">Let's read the datafile Seed_Data.csv and show the head of the file<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-read-the-datafile-Seed_Data.csv-and-show-the-head-of-the-file">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[2]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.4861px; left: 80.1528px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 262.569px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 67.1528px; top: 16.8889px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span> <span class="cm-operator">=</span> <span class="cm-variable">pd</span>.<span class="cm-property">read_csv</span>(<span class="cm-string">'Seed_Data.csv'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">head</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[2]:</bdi></div><div class="output_subarea output_html rendered_html output_result"><div>
<style scoped="">
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
      <th>A</th>
      <th>P</th>
      <th>C</th>
      <th>LK</th>
      <th>WK</th>
      <th>A_Coef</th>
      <th>LKG</th>
      <th>target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15.26</td>
      <td>14.84</td>
      <td>0.8710</td>
      <td>5.763</td>
      <td>3.312</td>
      <td>2.221</td>
      <td>5.220</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14.88</td>
      <td>14.57</td>
      <td>0.8811</td>
      <td>5.554</td>
      <td>3.333</td>
      <td>1.018</td>
      <td>4.956</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.29</td>
      <td>14.09</td>
      <td>0.9050</td>
      <td>5.291</td>
      <td>3.337</td>
      <td>2.699</td>
      <td>4.825</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13.84</td>
      <td>13.94</td>
      <td>0.8955</td>
      <td>5.324</td>
      <td>3.379</td>
      <td>2.259</td>
      <td>4.805</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.14</td>
      <td>14.99</td>
      <td>0.9034</td>
      <td>5.658</td>
      <td>3.562</td>
      <td>1.355</td>
      <td>5.175</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's check how many entries we have in the dataset</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-check-how-many-entries-we-have-in-the-dataset">Let's check how many entries we have in the dataset<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-check-how-many-entries-we-have-in-the-dataset">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[3]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 80.1528px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 77.8472px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 67.1528px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">info</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_text output_stream output_stdout"><pre>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 210 entries, 0 to 209
Data columns (total 8 columns):
A         210 non-null float64
P         210 non-null float64
C         210 non-null float64
LK        210 non-null float64
WK        210 non-null float64
A_Coef    210 non-null float64
LKG       210 non-null float64
target    210 non-null int64
dtypes: float64(7), int64(1)
memory usage: 13.2 KB
</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 254.042px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 254.042px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's display the basic statistic</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-display-the-basic-statistic">Let's display the basic statistic<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-display-the-basic-statistic">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[4]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 110.944px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 108.639px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 97.9444px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">describe</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[4]:</bdi></div><div class="output_subarea output_html rendered_html output_result"><div>
<style scoped="">
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
      <th>A</th>
      <th>P</th>
      <th>C</th>
      <th>LK</th>
      <th>WK</th>
      <th>A_Coef</th>
      <th>LKG</th>
      <th>target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>210.000000</td>
      <td>210.000000</td>
      <td>210.000000</td>
      <td>210.000000</td>
      <td>210.000000</td>
      <td>210.000000</td>
      <td>210.000000</td>
      <td>210.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>14.847524</td>
      <td>14.559286</td>
      <td>0.870999</td>
      <td>5.628533</td>
      <td>3.258605</td>
      <td>3.700201</td>
      <td>5.408071</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2.909699</td>
      <td>1.305959</td>
      <td>0.023629</td>
      <td>0.443063</td>
      <td>0.377714</td>
      <td>1.503557</td>
      <td>0.491480</td>
      <td>0.818448</td>
    </tr>
    <tr>
      <th>min</th>
      <td>10.590000</td>
      <td>12.410000</td>
      <td>0.808100</td>
      <td>4.899000</td>
      <td>2.630000</td>
      <td>0.765100</td>
      <td>4.519000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>12.270000</td>
      <td>13.450000</td>
      <td>0.856900</td>
      <td>5.262250</td>
      <td>2.944000</td>
      <td>2.561500</td>
      <td>5.045000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>14.355000</td>
      <td>14.320000</td>
      <td>0.873450</td>
      <td>5.523500</td>
      <td>3.237000</td>
      <td>3.599000</td>
      <td>5.223000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>17.305000</td>
      <td>15.715000</td>
      <td>0.887775</td>
      <td>5.979750</td>
      <td>3.561750</td>
      <td>4.768750</td>
      <td>5.877000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>21.180000</td>
      <td>17.250000</td>
      <td>0.918300</td>
      <td>6.675000</td>
      <td>4.033000</td>
      <td>8.456000</td>
      <td>6.550000</td>
      <td>2.000000</td>
    </tr>
  </tbody>
</table>
</div></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 28.4444px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 28.4444px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-hr">---</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="display: none; height: 39px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><hr>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h2"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 307.556px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 32px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 307.556px; top: 0px; height: 20.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-2">## Exploratory Data Analysis</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 32px;"></div><div class="CodeMirror-gutters" style="display: none; height: 43px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h2 id="Exploratory-Data-Analysis" data-toc-modified-id="Exploratory-Data-Analysis-1.2"><a class="toc-mod-link" id="Exploratory-Data-Analysis-1.2"></a><span class="toc-item-num">1.2&nbsp;&nbsp;</span>Exploratory Data Analysis<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Exploratory-Data-Analysis">¶</a></h2>
</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.0417px; left: 44.0833px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 44.0833px; top: 16.4444px; height: 17.3334px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">Let's see how the area 'A' relatedd to the compactness 'C', and create a scatter plot.</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="display: none; height: 56px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p>Let's see how the area 'A' relatedd to the compactness 'C', and create a scatter plot.</p>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[7]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 56.2639px; left: 18.5972px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 470.375px; margin-bottom: -19px; border-right-width: 11px; min-height: 79px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.59723px; top: 50.6667px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">sns</span>.<span class="cm-property">lmplot</span>(<span class="cm-variable">x</span><span class="cm-operator">=</span><span class="cm-string">'A'</span>, <span class="cm-variable">y</span><span class="cm-operator">=</span><span class="cm-string">'C'</span>, <span class="cm-variable">data</span><span class="cm-operator">=</span><span class="cm-variable">df</span>, <span class="cm-variable">hue</span><span class="cm-operator">=</span><span class="cm-string">'target'</span>,</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">          <span class="cm-variable">palette</span><span class="cm-operator">=</span><span class="cm-string">'Set1'</span>, <span class="cm-variable">height</span><span class="cm-operator">=</span><span class="cm-number">6</span>, <span class="cm-variable">aspect</span><span class="cm-operator">=</span><span class="cm-number">1</span>, <span class="cm-variable">fit_reg</span><span class="cm-operator">=</span><span class="cm-keyword">False</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span>()</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 79px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 90px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,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"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 452.319px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 452.319px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's see how area 'A' is related to A_Coef using scatter plot.</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-see-how-area-&#39;A&#39;-is-related-to-A_Coef-using-scatter-plot.">Let's see how area 'A' is related to A_Coef using scatter plot.<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-see-how-area-&#39;A&#39;-is-related-to-A_Coef-using-scatter-plot.">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[10]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 403.222px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1" draggable="false"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 485.764px; margin-bottom: -19px; border-right-width: 11px; min-height: 62px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre>x</pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"><div class="CodeMirror-selected" style="position: absolute; left: 344px; top: 0px; width: 46.2222px; height: 17px;"></div></div><div class="CodeMirror-cursors" style=""></div><div class="CodeMirror-code" role="presentation"><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">sns</span>.<span class="cm-property">lmplot</span>(<span class="cm-variable">x</span><span class="cm-operator">=</span><span class="cm-string">'A'</span>, <span class="cm-variable">y</span><span class="cm-operator">=</span><span class="cm-string">'A_Coef'</span>, <span class="cm-variable">data</span><span class="cm-operator">=</span><span class="cm-variable">df</span>, <span class="cm-variable">hue</span><span class="cm-operator">=</span><span class="cm-string">'target'</span>,</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">          <span class="cm-variable">palette</span><span class="cm-operator">=</span><span class="cm-string">'Set1'</span>, <span class="cm-variable">height</span><span class="cm-operator">=</span><span class="cm-number">6</span>, <span class="cm-variable">aspect</span><span class="cm-operator">=</span><span class="cm-number">1</span>, <span class="cm-variable">fit_reg</span> <span class="cm-operator">=</span> <span class="cm-keyword">False</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span>()</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 62px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 73px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,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"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[11]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 56.2639px; left: 87.8472px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true" style="display: block; right: 0px; left: 13px;"><div style="height: 100%; min-height: 1px; width: 655px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 655.014px; margin-bottom: -19px; border-right-width: 11px; min-height: 79px; padding-right: 0px; padding-bottom: 19px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 74.8472px; top: 50.6667px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">g</span> <span class="cm-operator">=</span> <span class="cm-variable">sns</span>.<span class="cm-property">FacetGrid</span>(<span class="cm-variable">data</span><span class="cm-operator">=</span><span class="cm-variable">df</span>, <span class="cm-variable">hue</span> <span class="cm-operator">=</span> <span class="cm-string">'target'</span>, <span class="cm-variable">palette</span> <span class="cm-operator">=</span> <span class="cm-string">'Set1'</span>, <span class="cm-variable">height</span> <span class="cm-operator">=</span> <span class="cm-number">6</span>, <span class="cm-variable">aspect</span> <span class="cm-operator">=</span> <span class="cm-number">2</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">g</span> <span class="cm-operator">=</span> <span class="cm-variable">g</span>.<span class="cm-property">map</span>(<span class="cm-variable">plt</span>.<span class="cm-property">hist</span>,<span class="cm-string">'A'</span>, <span class="cm-variable">bins</span><span class="cm-operator">=</span><span class="cm-number">20</span>, <span class="cm-variable">alpha</span><span class="cm-operator">=</span><span class="cm-number">0.5</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 19px solid transparent; top: 79px;"></div><div class="CodeMirror-gutters" style="left: -7.62939e-06px; height: 109px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA1gAAAGoCAYAAABbkkSYAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDMuMC4xLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvDW2N/gAAHNBJREFUeJzt3X9snId5H/AvKYrUD9uUXMlalNnTnHlv5aSYARdwGzWpkDhdYxftECBp0WbFfrjYhrToimLJ2iUoVnTAOqztmhZthjpB12JFsCbukLRI69lZssTDViSIsThmXntOPRtRLUuRzNgieeSRtz8o24or6Y7kI92d+fn8dUc8fO6588PX/Op97zjR6/UCAADA1k0OewAAAIBXCwELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAECRqavxII8//njvlltuuRoPxZh68sknc+TIkWGPwRixM2yUnWGj7AwbZWde9SYGKboqZ7C63e7VeBjG2OLi4rBHYMzYGTbKzrBRdoaNsjMkLhEEAAAoI2ABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCJTgxQ1TXNHkl9u2/Z40zS3JfmNJKtJOkl+vG3bk1dwRgAAgLHQ9wxW0zTvTXJvkl3nv/TrSX6qbdvjSe5L8r4rNh0AAMAYGeQSwSeSvOOC+z/Stu3D529PJVkqnwoAAGAMTfR6vb5FTdMcSfLRtm2/64KvvTHJh5O8uW3bU5f7/ocffrg3MzOzxVF5NVtaWsquXbv6F8J5doaNsjNs1Hbbmem9s1lem6jtOdnL8rn50p6jbLvtzHZz9OjRgX5ABnoP1is1TfPDSf5Vkrv7haskmZmZydGjRzfzUGwTc3NzdoQNsTNslJ1ho7bbzpw4u5hPP/z10p533/bavO6mw6U9R9l22xkubsMBq2madyf5J0mOt217pn4kAACA8bShj2lvmmZHkg8muTbJfU3TfKZpmn99RSYDAAAYMwOdwWrb9skkL77/6vorNg0AAMAY84eGAQAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAkalBipqmuSPJL7dte7xpmr+V5HeT9JI8kuQ9bduuXbkRAQAAxkPfM1hN07w3yb1Jdp3/0q8meX/btm9KMpHkh67ceAAAAONjkEsEn0jyjgvu357ks+dvfyrJndVDAQAAjKO+lwi2bfvxpmmOXPClibZte+dvP59ktl+PTqeTubm5zU24Tc3MzqSblb51U9mZznznKkx0ZS0tLdkRNsTOsFF2ho3adjuze19OnzpV2nJ+fm/mn3mytOco23Y7s80cPXp0oLqB3oP1Che+3+raJM/1+4aZmZmBB2LdyXMn8+BTD/Ste+tNd+bmwzdfhYmurLm5OTvChtgZNsrOsFHbbWdOnF3MgYMHS3vOzu7L4SOvKe05yrbbznBxm/kUwS81TXP8/O23J/lc3TgAAADjazNnsH42ye80TTOdZC7Jx2pHAgAAGE8DBay2bZ9M8l3nbz+W5Huv4EwAAABjyR8aBgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKDI17AEALrR69mx6L7zQt+6G7mq6Tz89UM+Ja67Jjv37tzoawEiZX1jOuc5qWb+V1bpesJ0JWMBI6b3wQhb+yx/2rZs/dSo7Dx4cqOeed70zEbCAV5lzndX8ycNfL+v3llsPlfWC7cwlggAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEWmNvNNTdPsTPKfkhxJsprkJ9q2/WrhXAAAAGNns2ew7koy1bbtG5P8YpJ/UzcSAADAeNpswHosyVTTNJNJrkuyUjcSAADAeNrUJYJJXsj65YFfTXIgyQ9crrjT6WRubm6TD7U97ZidzOnTp/rWzc8+lzNPnbkKE11ZS0tLdoQkyQ3d1cyf6r/73W43pweoS5IbFhbT+fIjWx3tWx9/10zOdLtl/a6fmsrUUqesX1I/47hznGGjRn5ndu8b+Dg4iOXl/aX9kmR+fm/mn3mytOcoG/mdYUuOHj06UN1mA9bPJPmztm1/rmmaG5N8umma72jbdulixTMzMwMPxLqT507mwIGDfetmZ/fl0OFDV2GiK2tubs6OkCTpPv10dh7sv/unT53KgQHqkmSmt5a1++/f6mjfYvZd78yhG28s69d9+uksfOKTZf2S+hnHneMMGzXqO3Pi7OLAx8FBTE9Pl/ZL1n9POXzkNaU9R9mo7wxXx2YD1tm8fFngmSQ7k+womQgAAGBMbTZg/VqSjzRN87kk00l+vm3bc3VjAQAAjJ9NBay2bV9I8q7iWQAAAMaaPzQMAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKTG32G5um+bkkP5hkOslvtW374bKpAAAAxtCmzmA1TXM8yRuTHEvyvUluLJwJAABgLG32DNbfTfLlJH+U5Lok/6JsIgAAgDG12YB1IMnfSPIDSf5mkk80TfPtbdv2Llbc6XQyNze3yYfannbMTub06VN96+Znn8uZp85chYmurKWlpcvuyMzsTLpZ6dtnKjvTme9UjsZVdkN3NfOn+u9+t9vN6QHqkuTQ8srAtYO6YWExnS8/UtZvenKifMbZ5+bz7AsvlPYcZ/2OM/BKI78zu/eVHjeWl/eXH4fm5/dm/pknS3uOspHfGbbk6NGjA9VtNmB9I8lX27ZdTtI2TbOU5GCSZy9WPDMzM/BArDt57mQOHDjYt252dl8OHT50FSa6subm5i67IyfPncyDTz3Qt89bb7ozNx++uXI0rrLu009n58H+u3/61KkcGKAuSaandw5cO6iZ3lrW7r+/rN+uu+8qn3HPvtl8242u4H5Rv+MMvNKo78yJs4ulx43p6eny49Ds7L4cPvKa0p6jbNR3hqtjs58i+Pkk3980zUTTNIeT7M166AIAANi2NhWw2rb94yRfSvLnST6Z5D1t265WDgYAADBuNv0x7W3bvrdyEAAAgHHnDw0DAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUmRr2AOPg+c7zWeguXLZmz9SeXDtz7VWa6GVrvbWcPHeyb92OiR1Z7a1etmbQ5zDI67HRfjtmJy/7PFbWVvr2GabnO8/n3MLZpNu9ZM3uTGfvUm/gnhPXXJMd+/dXjAdXxPzCcs51Ln9c2ai9Mzsyu2e6tCeMgivx87KyWtuPGo6NCFgDWOgu5MGnHrhszVtvunMoAWt5tZOHTjzUt+7Y4WN96wZ9DoO8Hhvt96dPfCoHDhy8ZM2xw8f69hmmhe5CHnjsj7PylUcvWfO2N7wjE597eOCee971zkTAYoSd66zmTx7+emnPu297bWb3lLaEkXAlfl7ecuuh0n7UcGzEJYIAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFprbyzU3T3JDki0ne1rbtV2tGAgAAGE+bPoPVNM3OJP8xyWLdOAAAAONrK5cI/vskH0pyomgWAACAsbapSwSbpvkHSU61bftnTdP8XL/6TqeTubm5zTzUSNgxO5nTp09dtmZ+9rmceerMVX3MJFk+uFxWN+hzGHS2jfTrdruX7Tno81y8YSGPzbd966ayM535Tt+6mdmZdLPSt25yekc6S50sLZy7ZM1SZynLp/o/hxfdsLCYzpcfGbh+EN1dMznT7Zb2vH5qKlNL/V/LQU1PTuT0AK9Tt9sdqC5JDi2vDFw7qOqeV2LG6h3auWd3VhZevmihs/f6LJ58dks916Z2ZHFt7aX78/N7M//Mk1vqeeFOrly7P4trE0mSmenr8hdf2/i/CfZ27Eintz7j9GQvy+fmtzTfOJreO5vl869jSb8xeR2Xlpbqfn/Zva/8Z3x5eX9pz+p+SbK4eH3m5p8r6zfqu7O0tJTMP1f+OlYcG9m6o0ePDlS32fdg/aMkvaZp7kxyW5Lfa5rmB9u2feZixTMzMwMPNIpOnjuZAwcOXrZmdnZfDh0+dFUfM0mmd06X1Q36HAadbSP9pqamLttz0Oc5MTWRLzz7hb51b73pztx8+OaBZnvwqQf61h07fCwzu2YyuWfvJWt2zezKdQf7P4cXzfTWsnb//QPXD2L2Xe/MoRtvLO3ZffrpLHzik2X9dt19Vw4M8DqdPnVqoLokmZ7eOXDtoKp7XokZq3do9913JRf0m7zjzZl84okt9Zx5/a3ZOzv70v3Z2X05fOQ1W+p54U6+cMeb8yefXf8FeWFhIXv27Nlwv52vvzWT52e8+7bX5nU3Hd7SfOPoxNnFfPrhr5f1G5fXcW5uruz3lxNnF6/AcWi6+DhU2y9JsmNnPv8Xdf8APeq7Mzc3l9nZfeWvY8WxkatnUwGrbds3v3i7aZrPJPmnlwpXAAAA24WPaQcAACiypY9pT5K2bY8XzAEAADD2nMECAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoMjXsAWAY1nprOXnuZN+6lbWVqzDNlbX8nW/I0u71H/WFmeXk1NcuWrc709m71Ntw/15neUvzsc31elmbn3/57rl96b5wemst7eTI6/V6OXF2sbTn3pkdmd0zXdZvfmE52b2vbM6V1dWSPtvdOOwOCFhsS8urnTx04qG+dccOH7sK01xZS7un8t8euS9JsrNzS1Yef/yidW97wzsy8bmHN9x/9913bWk+trluNyuPvbyT3QO9LPzv/7GllnZy9C2trObTj/b/R66NuPu212Z2T12/c53V/Nc/fzIHDh4s6feWWw+V9NnuxmF3wCWCAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARaY2801N0+xM8pEkR5LMJPmltm0/UTgXAADA2NnsGax3J/lG27ZvSvL2JL9ZNxIAAMB42tQZrCR/mORjF9zvFswCAAAw1jYVsNq2fSFJmqa5NutB6/2Xq+90Opmbm9vMQ42EHbOTOX361GVrFm9YyGPzbd9eu2Z2Z6mz2LducnrHRR9z9+RkJrurL91fPbCcxWef7dvvUnVrUzuyuLaWJJmffS5nnjrTt9cgr8dG+3W73cv2XD24sqXnebF+gzyH5YPLA9d1ljpZWjh3yZqlzlKWT/Xv9aJDyys5vYH6S1nrLGXh/FzXrK6+dHur872oas6N9ut2uwM/bvWMV6LnOM7YXVrKwsLClnqu7+TLPTpLS1ue+cI5L5xxbW1tU/PuWurk3PJ6v8XF6zM3/9yW5nul3TMzWex0RrZfkkxOTZfu0vLy/vJ9r/5vMzk1vaHjTD9X4jlX99yuM87P7838M0+W9FpaWkrmnxvpGZNkeu9sltcmyvpdiePO9GQvy+fmS3tu1dGjRweq2+wZrDRNc2OSP0ryW23b/sHlamdmZgYeaBSdPHcyBw4cvGzNxNREvvDsF/r2Onb42MB1F3vMtW/OZ6V97OXHPbKQySee6NvvUnUzr781e6+bTZLMzu7LocOH+vYa5PXYaL+pqanL9pycnNjS8/wr/b5jYqDnML1zeuC6mV0zmdyz95I1u2Z25bqD/Xu91HN6Zw5soP5SvjmzK3vOz7Vjx46Xbm91vhdVzbnRfqdPnRr4catnvBI9x3HGs7t2Zc+ePVvqub6TL/eY2bUr+7c484VzXjjjwsLCpubduWsmu2dnzw+8M5//i/7/cLQRb7n1mtKe1f1e7Fm7S9Pl+1793+Ytt16z/v+mojmvxHOu7rldZ5yd3ZfDR15T0mtubi6zs/tGesYkOXF2MZ9++Otl/a7Ecefu216b1910uLTn1bLZD7k4lOT+JD/Ztu2DtSMBAACMp82ewfr5JPuTfKBpmg+c/9rb27btf+0bAADAq9Rm34P100l+ungWAACAseYPDQMAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABSZGvYAw/R85/ksdBf61q2srVyFaYZvrbeWk+dO9q3r93r0lhbTW17O2nInzyx8rW+/7o5k71ova9+cv3TRwV7fPqNu4uCBfPNNt/Wt27nv+qw8dybnrpvM6mXqX6zrZ+3A/g3NCbxCr5e1+fXjU6/7bS/d3pLJyWRtra5ndb8kE9PTmdi9e8t9YNT1er2cOLtY02z3vqysrtb0Ymxt64C10F3Ig0890Lfu2OFjV2Ga4Vte7eShEw/1rev3evSWl7PylUez9NfemM88eG/ffsffek+Wvvx/Mrln76WLXve2vn1G3fLkWj7zyH19646/9Z585pH7srNzS1Yef7xv3SD9gC3odrPy2PrPYu/oDVn5yqNbbrnzb99S2rO6X5LsfP2tAhbbwtLKaj79aP9/YB7E6VOn8q7vfUNJL8aXSwQBAACKCFgAAABFBCwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIoIWAAAAEUELAAAgCICFgAAQBEBCwAAoIiABQAAUETAAgAAKCJgAQAAFBGwAAAAighYAAAARQQsAACAIgIWAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAAACKTG3mm5qmmUzyW0n+TpJOknvatv2/lYMBAACMm82ewfp7SXa1bfvdSf5lkl+pGwkAAGA8bTZgfU+SP02Stm3/V5LvLJsIAABgTE30er0Nf1PTNPcm+Xjbtp86f/+pJDe3bdu9WP0Xv/jFU0n+31YGBQAAGKLTt99++/f3K9rUe7CSfDPJtRfcn7xUuEqS22+//eAmHwcAAGBsbPYSwYeS3JUkTdN8V5Ivl00EAAAwpjZ7BuuPkrytaZr/mWQiyT+sGwkAAGA8beo9WAAAAPxV/tAwAABAEQELAACgiIAFAABQZLMfcgFb1jTNHUl+uW3b403T3JbkN5KsJukk+fG2bU8OdUBGyoX7csHXfjTJT7Vt+91DG4yR9YpjzA1JfifJ/iQ7sn6MeWKoAzJyLvL/pQ8l6SZ5LMk9bduuDXVARkbTNDuTfCTJkSQzSX4pyaNJfjdJL8kjSd5jZ7YnZ7AYiqZp3pvk3iS7zn/p17P+i/LxJPcled+QRmMEXWRfcv6Xn3+c9U8yhW9xkZ35d0n+c9u2b07y/iTfPqzZGE0X2ZlfSPKLbdt+T9Z/gb57WLMxkt6d5Btt274pyduT/GaSX03y/vNfm0jyQ0OcjyESsBiWJ5K844L7P9K27cPnb08lWbr6IzHCvmVfmqb5tiT/Nsk/H9pEjLpXHmOOJfnrTdM8kOTHknxmGEMx0l65M19Kcn3TNBNJrk2yMpSpGFV/mOQDF9zvJrk9yWfP3/9Ukjuv9lCMBgGLoWjb9uO54H9Wbdv+ZZI0TfPGJD+Z5NeGNBoj6MJ9aZpmR5IPJ/mZJM8Pcy5G1yuPMVm/jOds27Z3JnkqzpLzChfZmceTfDDJXJJDEcq5QNu2L7Rt+3zTNNcm+VjWz4xPtG374t8/ej7J7NAGZKgELEZG0zQ/nPXr3e9u2/bUsOdhZN2e5JYkv53ko0lubZrmPwx3JMbAN5J84vztTyb5ziHOwnj49SRvatv225P8XpJfGfI8jJimaW5M8t+T/H7btn+Q5ML3W12b5LmhDMbQCViMhKZp3p31M1fH27b92rDnYXS1bfvnbdu+/vz79X4kyaNt27pUkH4+n+Su87ffnOQrQ5yF8XAmyTfP3z6R9Q9IgSRJ0zSHktyf5H1t237k/Je/1DTN8fO3357kc8OYjeHzKYIM3flLvj6Y9ct27muaJkk+27btLwx1MODV5GeT3Ns0zT9LMp/kR4c8D6PvniQfbZqmm2Q5yU8MeR5Gy89nPXR/oGmaF9+L9dNJPtg0zXTWLy392LCGY7gmer1e/yoAAAD6cokgAABAEQELAACgiIAFAABQRMACAAAoImABAAAUEbAAGHtN07yvaZq/bJpm17BnAWB7E7AAeDX4sSQfzfofnwaAoRGwABhrTdMcT/JEkg8lec9wpwFguxOwABh39yS5t23bNkmnaZo7hj0QANvXRK/XG/YMALApTdPsz/rZqy8kWUvy2iQPt23794c6GADbljNYAIyzdyf5cNu239e27fcnuSPJ9zVNc3DIcwGwTQlYAIyze5L8/ot32rZdSPLxJD8xtIkA2NZcIggAAFDEGSwAAIAiAhYAAEARAQsAAKCIgAUAAFBEwAIAACgiYAEAABQRsAAAAIr8f21ik0iMUooJAAAAAElFTkSuQmCC"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 28.4444px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 28.4444px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-hr">---</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="display: none; height: 39px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><hr>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h2"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 32px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 20.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-2">## KMEANS CLUSTERING</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 32px;"></div><div class="CodeMirror-gutters" style="display: none; height: 43px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h2 id="KMEANS-CLUSTERING" data-toc-modified-id="KMEANS-CLUSTERING-1.3"><a class="toc-mod-link" id="KMEANS-CLUSTERING-1.3"></a><span class="toc-item-num">1.3&nbsp;&nbsp;</span>KMEANS CLUSTERING<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#KMEANS-CLUSTERING">¶</a></h2>
</div></div></div><div class="cell text_cell rendered unselected" tabindex="2"><div class="prompt input_prompt"></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 490.514px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors"><div class="CodeMirror-cursor" style="left: 490.514px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">Machine learning using KMEANS clustering unsupervised algorithm</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="display: none; height: 39px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><p>Machine learning using KMEANS clustering unsupervised algorithm</p>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59717px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's import KMeans from Scikit-learn and create an instance of KMeans model with 3 clusters.</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="display: none; height: 58px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-import-KMeans-from-Scikit-learn-and-create-an-instance-of-KMeans-model-with-3-clusters.">Let's import KMeans from Scikit-learn and create an instance of KMeans model with 3 clusters.<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-import-KMeans-from-Scikit-learn-and-create-an-instance-of-KMeans-model-with-3-clusters.">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[13]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.4861px; left: 218.708px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 270.264px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 205.708px; top: 16.8889px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">from</span> <span class="cm-variable">sklearn</span>.<span class="cm-property">cluster</span> <span class="cm-keyword">import</span> <span class="cm-variable">KMeans</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">kmeans</span> <span class="cm-operator">=</span> <span class="cm-variable">KMeans</span>(<span class="cm-variable">n_clusters</span><span class="cm-operator">=</span><span class="cm-number">3</span>)</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 382px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 382px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's fit the model to all data except for the 'target'</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-fit-the-model-to-all-data-except-for-the-&#39;target&#39;">Let's fit the model to all data except for the 'target'<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-fit-the-model-to-all-data-except-for-the-&#39;target&#39;">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[14]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 295.625px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 285.625px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"><pre><span>xxxxxxxxxx</span></pre></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 282.625px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">kmeans</span>.<span class="cm-property">fit</span><span class=" CodeMirror-matchingbracket">(</span><span class="cm-variable">df</span>.<span class="cm-property">drop</span>(<span class="cm-string">'target'</span>,<span class="cm-variable">axis</span><span class="cm-operator">=</span><span class="cm-number">1</span>)<span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[14]:</bdi></div><div class="output_subarea output_text output_result"><pre>KMeans(algorithm='auto', copy_x=True, init='k-means++', max_iter=300,
    n_clusters=3, n_init=10, n_jobs=None, precompute_distances='auto',
    random_state=None, tol=0.0001, verbose=0)</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 23.375px; left: 77.125px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 77.125px; top: 17.7777px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's figure out how to get the cluster center vectors, and pass them to 'centers', then the ouput. </span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="display: none; height: 58px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-figure-out-how-to-get-the-cluster-center-vectors,-and-pass-them-to-&#39;centers&#39;,-then-the-ouput.">Let's figure out how to get the cluster center vectors, and pass them to 'centers', then the ouput.<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-figure-out-how-to-get-the-cluster-center-vectors,-and-pass-them-to-&#39;centers&#39;,-then-the-ouput.">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[15]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.4861px; left: 72.4722px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 262.556px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 59.4722px; top: 16.8889px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">centers</span> <span class="cm-operator">=</span> <span class="cm-variable">kmeans</span>.<span class="cm-property">cluster_centers_</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">centers</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[15]:</bdi></div><div class="output_subarea output_text output_result"><pre>array([[18.72180328, 16.29737705,  0.88508689,  6.20893443,  3.72267213,
         3.60359016,  6.06609836],
       [11.96441558, 13.27480519,  0.8522    ,  5.22928571,  2.87292208,
         4.75974026,  5.08851948],
       [14.64847222, 14.46041667,  0.87916667,  5.56377778,  3.27790278,
         2.64893333,  5.19231944]])</pre></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 23.375px; left: 514.264px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 47px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 514.264px; top: 17.7777px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### now that we have the fitted model, let's get the labels for kmean and create a new column 'klabels' in our dataframe, and let's check the head of our dataframe </span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 47px;"></div><div class="CodeMirror-gutters" style="display: none; height: 58px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="now-that-we-have-the-fitted-model,-let&#39;s-get-the-labels-for-kmean-and-create-a-new-column-&#39;klabels&#39;-in-our-dataframe,-and-let&#39;s-check-the-head-of-our-dataframe">now that we have the fitted model, let's get the labels for kmean and create a new column 'klabels' in our dataframe, and let's check the head of our dataframe<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#now-that-we-have-the-fitted-model,-let&#39;s-get-the-labels-for-kmean-and-create-a-new-column-&#39;klabels&#39;-in-our-dataframe,-and-let&#39;s-check-the-head-of-our-dataframe">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[16]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 22.4861px; left: 87.8472px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 239.444px; margin-bottom: -19px; border-right-width: 11px; min-height: 45px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 74.8472px; top: 16.8889px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>[<span class="cm-string">'klabels'</span>] <span class="cm-operator">=</span> <span class="cm-variable">kmeans</span>.<span class="cm-property">labels_</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">df</span>.<span class="cm-property">head</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 45px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 56px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt output_prompt"><bdi>Out[16]:</bdi></div><div class="output_subarea output_html rendered_html output_result"><div>
<style scoped="">
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
      <th>A</th>
      <th>P</th>
      <th>C</th>
      <th>LK</th>
      <th>WK</th>
      <th>A_Coef</th>
      <th>LKG</th>
      <th>target</th>
      <th>klabels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15.26</td>
      <td>14.84</td>
      <td>0.8710</td>
      <td>5.763</td>
      <td>3.312</td>
      <td>2.221</td>
      <td>5.220</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>14.88</td>
      <td>14.57</td>
      <td>0.8811</td>
      <td>5.554</td>
      <td>3.333</td>
      <td>1.018</td>
      <td>4.956</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14.29</td>
      <td>14.09</td>
      <td>0.9050</td>
      <td>5.291</td>
      <td>3.337</td>
      <td>2.699</td>
      <td>4.825</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13.84</td>
      <td>13.94</td>
      <td>0.8955</td>
      <td>5.324</td>
      <td>3.379</td>
      <td>2.259</td>
      <td>4.805</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.14</td>
      <td>14.99</td>
      <td>0.9034</td>
      <td>5.658</td>
      <td>3.562</td>
      <td>1.355</td>
      <td>5.175</td>
      <td>0</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's create a plot </span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-create-a-plot">Let's create a plot<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-create-a-plot">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[22]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 140.708px; left: 203.306px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 477.667px; margin-bottom: -19px; border-right-width: 11px; min-height: 282px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 190.306px; top: 135.111px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">fig</span>, (<span class="cm-variable">ax1</span>, <span class="cm-variable">ax2</span>) <span class="cm-operator">=</span> <span class="cm-variable">plt</span>.<span class="cm-property">subplots</span>(<span class="cm-variable">nrows</span> <span class="cm-operator">=</span> <span class="cm-number">1</span>, <span class="cm-variable">ncols</span> <span class="cm-operator">=</span> <span class="cm-number">2</span>,</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">                             <span class="cm-variable">sharey</span> <span class="cm-operator">=</span> <span class="cm-keyword">True</span>, <span class="cm-variable">figsize</span> <span class="cm-operator">=</span> (<span class="cm-number">10</span>,<span class="cm-number">6</span>))</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-comment"># For fitted with kmeans </span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">ax1</span>.<span class="cm-property">set_title</span>(<span class="cm-string">'K Means (K = 3)'</span>)</span></pre><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">ax1</span>.<span class="cm-property">scatter</span>(<span class="cm-variable">x</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[<span class="cm-string">'A'</span>], <span class="cm-variable">y</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[<span class="cm-string">'A_Coef'</span>], </span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">            <span class="cm-variable">c</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[<span class="cm-string">'klabels'</span>], <span class="cm-variable">cmap</span><span class="cm-operator">=</span><span class="cm-string">'rainbow'</span>)</span></pre><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">ax1</span>.<span class="cm-property">scatter</span>(<span class="cm-variable">x</span><span class="cm-operator">=</span><span class="cm-variable">centers</span>[:, <span class="cm-number">0</span>], <span class="cm-variable">y</span><span class="cm-operator">=</span><span class="cm-variable">centers</span>[:, <span class="cm-number">5</span>],</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">            <span class="cm-variable">c</span><span class="cm-operator">=</span><span class="cm-string">'black'</span>, <span class="cm-variable">s</span> <span class="cm-operator">=</span><span class="cm-number">300</span>, <span class="cm-variable">alpha</span><span class="cm-operator">=</span><span class="cm-number">0.5</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-comment"># For original data </span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">ax2</span>.<span class="cm-property">set_title</span>(<span class="cm-string">"Original"</span>)</span></pre><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">ax2</span>.<span class="cm-property">scatter</span>(<span class="cm-variable">x</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[<span class="cm-string">'A'</span>], <span class="cm-variable">y</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[<span class="cm-string">'A_Coef'</span>], </span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">            <span class="cm-variable">c</span> <span class="cm-operator">=</span> <span class="cm-variable">df</span>[<span class="cm-string">'target'</span>], <span class="cm-variable">cmap</span><span class="cm-operator">=</span><span class="cm-string">'rainbow'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span>()</span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 282px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 293px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,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"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h2"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 5.33333px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 32px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.33333px; top: 0px; height: 20.4444px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-2">## Elbow point</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 32px;"></div><div class="CodeMirror-gutters" style="display: none; height: 43px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h2 id="Elbow-point" data-toc-modified-id="Elbow-point-1.4"><a class="toc-mod-link" id="Elbow-point-1.4"></a><span class="toc-item-num">1.4&nbsp;&nbsp;</span>Elbow point<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Elbow-point">¶</a></h2>
</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 482.667px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true" style="bottom: 0px;"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 482.667px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's etimate the Elbow point to see our selection for K was right.</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-etimate-the-Elbow-point-to-see-our-selection-for-K-was-right.">Let's etimate the Elbow point to see our selection for K was right.<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-etimate-the-Elbow-point-to-see-our-selection-for-K-was-right.">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[23]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 106.931px; left: 295.653px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true" style="display: block; right: 0px; left: 13px;"><div style="height: 100%; min-height: 1px; width: 732px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 731.889px; margin-bottom: -19px; border-right-width: 11px; min-height: 130px; padding-right: 0px; padding-bottom: 19px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 282.653px; top: 101.333px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-comment"># sum_square will be key,value pair for the elbow plot!</span></span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">sum_square</span> <span class="cm-operator">=</span> {}</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-comment"># Let's test for K from 1 to 10, we can use range() function here! remember?</span></span></pre><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-keyword">for</span> <span class="cm-variable">k</span> <span class="cm-keyword">in</span> <span class="cm-builtin">range</span>(<span class="cm-number">1</span>, <span class="cm-number">10</span>):</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">kmeans</span> <span class="cm-operator">=</span> <span class="cm-variable">KMeans</span>(<span class="cm-variable">n_clusters</span><span class="cm-operator">=</span><span class="cm-variable">k</span>).<span class="cm-property">fit</span>(<span class="cm-variable">df</span>.<span class="cm-property">drop</span>(<span class="cm-string">'target'</span>,<span class="cm-variable">axis</span><span class="cm-operator">=</span><span class="cm-number">1</span>))</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-comment"># .inertia: Computing Sum of Squared Distances of samples to their closest cluster center.</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">    <span class="cm-variable">sum_square</span>[<span class="cm-variable">k</span>] <span class="cm-operator">=</span> <span class="cm-variable">kmeans</span>.<span class="cm-property">inertia_</span> </span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 19px solid transparent; top: 130px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 160px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell text_cell collapsible_headings_ellipsis rendered unselected" tabindex="2"><div class="prompt input_prompt"><div class="collapsible_headings_toggle" style="color: rgb(170, 170, 170);"><div class="h5"><i class="fa fa-fw fa-caret-down"></i></div></div></div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-default CodeMirror-wrap"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 233px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 0px; margin-bottom: -19px; border-right-width: 11px; min-height: 29px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 233px; top: 0px; height: 17.7778px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-header cm-header-5">##### Let's generate a Elbow plot </span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 29px;"></div><div class="CodeMirror-gutters" style="display: none; height: 40px;"></div></div></div></div><div class="text_cell_render rendered_html" tabindex="-1"><h5 id="Let&#39;s-generate-a-Elbow-plot">Let's generate a Elbow plot<a class="anchor-link" href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#Let&#39;s-generate-a-Elbow-plot">¶</a></h5>
</div></div></div><div class="cell code_cell rendered unselected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[25]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 140.708px; left: 95.5417px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 277.667px; margin-bottom: -19px; border-right-width: 11px; min-height: 164px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style=""><div class="CodeMirror-cursor" style="left: 82.5417px; top: 135.111px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation" style=""><div style="position: relative;"><div class="CodeMirror-gutter-wrapper" style="left: -13px;"><div class="CodeMirror-gutter-elt" style="left: 0px; width: 12px;"><div class="CodeMirror-foldgutter-open CodeMirror-guttermarker-subtle"></div></div></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">plot</span>(<span class="cm-builtin">list</span>(<span class="cm-variable">sum_square</span>.<span class="cm-property">keys</span>()),</span></pre></div><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">         <span class="cm-builtin">list</span>(<span class="cm-variable">sum_square</span>.<span class="cm-property">values</span>()),</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">        <span class="cm-variable">linestyle</span> <span class="cm-operator">=</span> <span class="cm-string">'-'</span>,</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">        <span class="cm-variable">marker</span> <span class="cm-operator">=</span> <span class="cm-string">'H'</span>,</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">        <span class="cm-variable">color</span> <span class="cm-operator">=</span> <span class="cm-string">'g'</span>,</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">        <span class="cm-variable">markersize</span> <span class="cm-operator">=</span> <span class="cm-number">8</span>,</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;">        <span class="cm-variable">markerfacecolor</span> <span class="cm-operator">=</span><span class="cm-string">'b'</span>)</span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span class="cm-variable">plt</span>.<span class="cm-property">show</span><span class=" CodeMirror-matchingbracket">(</span><span class=" CodeMirror-matchingbracket">)</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 164px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 175px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to scroll output; double click to hide"></div><div class="output"><div class="output_area"><div class="run_this_cell"></div><div class="prompt"></div><div class="output_subarea output_png"><img src="data:image/png;base64,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"></div></div></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div><div class="cell code_cell unrendered selected" tabindex="2"><div class="input"><div class="run_this_cell" title="Run this cell"><i class="fa-step-forward fa"></i></div><div class="prompt input_prompt"><bdi>In</bdi>&nbsp;[&nbsp;]:</div><div class="inner_cell"><div class="ctb_hideshow"><div class="celltoolbar"></div></div><div class="input_area"><div class="CodeMirror cm-s-ipython"><div style="overflow: hidden; position: relative; width: 3px; height: 0px; top: 5.59723px; left: 18.5972px;"><textarea autocorrect="off" autocapitalize="off" spellcheck="false" tabindex="0" style="position: absolute; bottom: -1em; padding: 0px; width: 1000px; height: 1em; outline: none;"></textarea></div><div class="CodeMirror-vscrollbar" cm-not-content="true"><div style="min-width: 1px; height: 0px;"></div></div><div class="CodeMirror-hscrollbar" cm-not-content="true"><div style="height: 100%; min-height: 1px; width: 0px;"></div></div><div class="CodeMirror-scrollbar-filler" cm-not-content="true"></div><div class="CodeMirror-gutter-filler" cm-not-content="true"></div><div class="CodeMirror-scroll" tabindex="-1"><div class="CodeMirror-sizer" style="margin-left: 13px; min-width: 8.59723px; margin-bottom: -19px; border-right-width: 11px; min-height: 28px; padding-right: 0px; padding-bottom: 0px;"><div style="position: relative; top: 0px;"><div class="CodeMirror-lines" role="presentation"><div role="presentation" style="position: relative; outline: none;"><div class="CodeMirror-measure"></div><div class="CodeMirror-measure"></div><div style="position: relative; z-index: 1;"></div><div class="CodeMirror-cursors" style="visibility: hidden;"><div class="CodeMirror-cursor" style="left: 5.59723px; top: 0px; height: 16.8889px;">&nbsp;</div></div><div class="CodeMirror-code" role="presentation"><pre class=" CodeMirror-line " role="presentation"><span role="presentation" style="padding-right: 0.1px;"><span cm-text="">​</span></span></pre></div></div></div></div></div><div style="position: absolute; height: 11px; width: 1px; border-bottom: 0px solid transparent; top: 28px;"></div><div class="CodeMirror-gutters" style="left: 0px; height: 39px;"><div class="CodeMirror-gutter CodeMirror-foldgutter"></div></div></div></div></div></div></div><div class="output_wrapper"><div class="out_prompt_overlay prompt" title="click to expand output; double click to hide output"></div><div class="output"></div><div class="btn btn-default output_collapsed" title="click to expand output" style="display: none;">. . .</div></div></div></div><div class="end_space"></div></div>
        <div id="tooltip" class="ipython_tooltip" style="left: 145.208px; top: 3068.65px; display: none;"><div class="tooltipbuttons"><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" role="button" class="ui-button"><span class="ui-icon ui-icon-close">Close</span></a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="ui-corner-all" role="button" id="expanbutton" title="Grow the tooltip vertically (press shift-tab twice)"><span class="ui-icon ui-icon-plus">Expand</span></a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" role="button" class="ui-button" title="show the current docstring in pager (press shift-tab 4 times)"><span class="ui-icon ui-icon-arrowstop-l-n">Open in Pager</span></a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" role="button" class="ui-button" title="Tooltip will linger for 10 seconds while you type" style="display: none;"><span class="ui-icon ui-icon-clock">Close</span></a></div><div class="pretooltiparrow" style="left: 266.319px;"></div><div class="tooltiptext smalltooltip"><pre><span class="ansi-red-intense-fg ansi-bold">Init signature:</span> sns<span class="ansi-yellow-intense-fg ansi-bold">.</span>FacetGrid<span class="ansi-yellow-intense-fg ansi-bold">(</span>data<span class="ansi-yellow-intense-fg ansi-bold">,</span> row<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> col<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> hue<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> col_wrap<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> sharex<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">True</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> sharey<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">True</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> height<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-cyan-intense-fg ansi-bold">3</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> aspect<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-cyan-intense-fg ansi-bold">1</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> palette<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> row_order<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> col_order<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> hue_order<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> hue_kws<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> dropna<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">True</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> legend_out<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">True</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> despine<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">True</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> margin_titles<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">False</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> xlim<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> ylim<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> subplot_kws<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> gridspec_kws<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">,</span> size<span class="ansi-yellow-intense-fg ansi-bold">=</span><span class="ansi-green-intense-fg ansi-bold">None</span><span class="ansi-yellow-intense-fg ansi-bold">)</span>
<span class="ansi-red-intense-fg ansi-bold">Docstring:</span>      Multi-plot grid for plotting conditional relationships.
<span class="ansi-red-intense-fg ansi-bold">Init docstring:</span>
Initialize the matplotlib figure and FacetGrid object.

This class maps a dataset onto multiple axes arrayed in a grid of rows
and columns that correspond to *levels* of variables in the dataset.
The plots it produces are often called "lattice", "trellis", or
"small-multiple" graphics.

It can also represent levels of a third varaible with the ``hue``
parameter, which plots different subets of data in different colors.
This uses color to resolve elements on a third dimension, but only
draws subsets on top of each other and will not tailor the ``hue``
parameter for the specific visualization the way that axes-level
functions that accept ``hue`` will.

When using seaborn functions that infer semantic mappings from a
dataset, care must be taken to synchronize those mappings across
facets. In most cases, it will be better to use a figure-level function
(e.g. :func:`relplot` or :func:`catplot`) than to use
:class:`FacetGrid` directly.

The basic workflow is to initialize the :class:`FacetGrid` object with
the dataset and the variables that are used to structure the grid. Then
one or more plotting functions can be applied to each subset by calling
:meth:`FacetGrid.map` or :meth:`FacetGrid.map_dataframe`. Finally, the
plot can be tweaked with other methods to do things like change the
axis labels, use different ticks, or add a legend. See the detailed
code examples below for more information.

See the :ref:`tutorial &lt;grid_tutorial&gt;` for more information.

Parameters
----------
data : DataFrame
    Tidy ("long-form") dataframe where each column is a variable and each
    row is an observation.    
row, col, hue : strings
    Variables that define subsets of the data, which will be drawn on
    separate facets in the grid. See the ``*_order`` parameters to
    control the order of levels of this variable.
col_wrap : int, optional
    "Wrap" the column variable at this width, so that the column facets
    span multiple rows. Incompatible with a ``row`` facet.    
share{x,y} : bool, 'col', or 'row' optional
    If true, the facets will share y axes across columns and/or x axes
    across rows.    
height : scalar, optional
    Height (in inches) of each facet. See also: ``aspect``.    
aspect : scalar, optional
    Aspect ratio of each facet, so that ``aspect * height`` gives the width
    of each facet in inches.    
palette : palette name, list, or dict, optional
    Colors to use for the different levels of the ``hue`` variable. Should
    be something that can be interpreted by :func:`color_palette`, or a
    dictionary mapping hue levels to matplotlib colors.    
{row,col,hue}_order : lists, optional
    Order for the levels of the faceting variables. By default, this
    will be the order that the levels appear in ``data`` or, if the
    variables are pandas categoricals, the category order.
hue_kws : dictionary of param -&gt; list of values mapping
    Other keyword arguments to insert into the plotting call to let
    other plot attributes vary across levels of the hue variable (e.g.
    the markers in a scatterplot).
legend_out : bool, optional
    If ``True``, the figure size will be extended, and the legend will be
    drawn outside the plot on the center right.    
despine : boolean, optional
    Remove the top and right spines from the plots.
margin_titles : bool, optional
    If ``True``, the titles for the row variable are drawn to the right of
    the last column. This option is experimental and may not work in all
    cases.    
{x, y}lim: tuples, optional
    Limits for each of the axes on each facet (only relevant when
    share{x, y} is True.
subplot_kws : dict, optional
    Dictionary of keyword arguments passed to matplotlib subplot(s)
    methods.
gridspec_kws : dict, optional
    Dictionary of keyword arguments passed to matplotlib's ``gridspec``
    module (via ``plt.subplots``). Requires matplotlib &gt;= 1.4 and is
    ignored if ``col_wrap`` is not ``None``.

See Also
--------
PairGrid : Subplot grid for plotting pairwise relationships.
relplot : Combine a relational plot and a :class:`FacetGrid`.
catplot : Combine a categorical plot and a :class:`FacetGrid`.
lmplot : Combine a regression plot and a :class:`FacetGrid`.

Examples
--------

Initialize a 2x2 grid of facets using the tips dataset:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; import seaborn as sns; sns.set(style="ticks", color_codes=True)
    &gt;&gt;&gt; tips = sns.load_dataset("tips")
    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="time", row="smoker")

Draw a univariate plot on each facet:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; import matplotlib.pyplot as plt
    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="time",  row="smoker")
    &gt;&gt;&gt; g = g.map(plt.hist, "total_bill")

(Note that it's not necessary to re-catch the returned variable; it's
the same object, but doing so in the examples makes dealing with the
doctests somewhat less annoying).

Pass additional keyword arguments to the mapped function:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; import numpy as np
    &gt;&gt;&gt; bins = np.arange(0, 65, 5)
    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="time",  row="smoker")
    &gt;&gt;&gt; g = g.map(plt.hist, "total_bill", bins=bins, color="r")

Plot a bivariate function on each facet:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="time",  row="smoker")
    &gt;&gt;&gt; g = g.map(plt.scatter, "total_bill", "tip", edgecolor="w")

Assign one of the variables to the color of the plot elements:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="time",  hue="smoker")
    &gt;&gt;&gt; g = (g.map(plt.scatter, "total_bill", "tip", edgecolor="w")
    ...       .add_legend())

Change the height and aspect ratio of each facet:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="day", height=4, aspect=.5)
    &gt;&gt;&gt; g = g.map(plt.hist, "total_bill", bins=bins)

Specify the order for plot elements:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="smoker", col_order=["Yes", "No"])
    &gt;&gt;&gt; g = g.map(plt.hist, "total_bill", bins=bins, color="m")

Use a different color palette:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; kws = dict(s=50, linewidth=.5, edgecolor="w")
    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="sex", hue="time", palette="Set1",
    ...                   hue_order=["Dinner", "Lunch"])
    &gt;&gt;&gt; g = (g.map(plt.scatter, "total_bill", "tip", **kws)
    ...      .add_legend())

Use a dictionary mapping hue levels to colors:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; pal = dict(Lunch="seagreen", Dinner="gray")
    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="sex", hue="time", palette=pal,
    ...                   hue_order=["Dinner", "Lunch"])
    &gt;&gt;&gt; g = (g.map(plt.scatter, "total_bill", "tip", **kws)
    ...      .add_legend())

Additionally use a different marker for the hue levels:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="sex", hue="time", palette=pal,
    ...                   hue_order=["Dinner", "Lunch"],
    ...                   hue_kws=dict(marker=["^", "v"]))
    &gt;&gt;&gt; g = (g.map(plt.scatter, "total_bill", "tip", **kws)
    ...      .add_legend())

"Wrap" a column variable with many levels into the rows:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; att = sns.load_dataset("attention")
    &gt;&gt;&gt; g = sns.FacetGrid(att, col="subject", col_wrap=5, height=1.5)
    &gt;&gt;&gt; g = g.map(plt.plot, "solutions", "score", marker=".")

Define a custom bivariate function to map onto the grid:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; from scipy import stats
    &gt;&gt;&gt; def qqplot(x, y, **kwargs):
    ...     _, xr = stats.probplot(x, fit=False)
    ...     _, yr = stats.probplot(y, fit=False)
    ...     plt.scatter(xr, yr, **kwargs)
    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="smoker", hue="sex")
    &gt;&gt;&gt; g = (g.map(qqplot, "total_bill", "tip", **kws)
    ...       .add_legend())

Define a custom function that uses a ``DataFrame`` object and accepts
column names as positional variables:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; import pandas as pd
    &gt;&gt;&gt; df = pd.DataFrame(
    ...     data=np.random.randn(90, 4),
    ...     columns=pd.Series(list("ABCD"), name="walk"),
    ...     index=pd.date_range("2015-01-01", "2015-03-31",
    ...                         name="date"))
    &gt;&gt;&gt; df = df.cumsum(axis=0).stack().reset_index(name="val")
    &gt;&gt;&gt; def dateplot(x, y, **kwargs):
    ...     ax = plt.gca()
    ...     data = kwargs.pop("data")
    ...     data.plot(x=x, y=y, ax=ax, grid=False, **kwargs)
    &gt;&gt;&gt; g = sns.FacetGrid(df, col="walk", col_wrap=2, height=3.5)
    &gt;&gt;&gt; g = g.map_dataframe(dateplot, "date", "val")

Use different axes labels after plotting:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="smoker", row="sex")
    &gt;&gt;&gt; g = (g.map(plt.scatter, "total_bill", "tip", color="g", **kws)
    ...       .set_axis_labels("Total bill (US Dollars)", "Tip"))

Set other attributes that are shared across the facetes:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="smoker", row="sex")
    &gt;&gt;&gt; g = (g.map(plt.scatter, "total_bill", "tip", color="r", **kws)
    ...       .set(xlim=(0, 60), ylim=(0, 12),
    ...            xticks=[10, 30, 50], yticks=[2, 6, 10]))

Use a different template for the facet titles:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="size", col_wrap=3)
    &gt;&gt;&gt; g = (g.map(plt.hist, "tip", bins=np.arange(0, 13), color="c")
    ...       .set_titles("{col_name} diners"))

Tighten the facets:

.. plot::
    :context: close-figs

    &gt;&gt;&gt; g = sns.FacetGrid(tips, col="smoker", row="sex",
    ...                   margin_titles=True)
    &gt;&gt;&gt; g = (g.map(plt.scatter, "total_bill", "tip", color="m", **kws)
    ...       .set(xlim=(0, 60), ylim=(0, 12),
    ...            xticks=[10, 30, 50], yticks=[2, 6, 10])
    ...       .fig.subplots_adjust(wspace=.05, hspace=.05))
<span class="ansi-red-intense-fg ansi-bold">File:</span>           c:\users\stevy\anaconda3\lib\site-packages\seaborn\axisgrid.py
<span class="ansi-red-intense-fg ansi-bold">Type:</span>           type
</pre></div></div>
    </div>
</div>



</div>



<div id="pager" class="ui-resizable">
    <div id="pager-contents">
        <div id="pager-container" class="container"></div>
    </div>
    <div id="pager-button-area"><a role="button" title="Open the pager in an external window" class="ui-button"><span class="ui-icon ui-icon-extlink"></span></a><a role="button" title="Close the pager" class="ui-button"><span class="ui-icon ui-icon-close"></span></a></div>
<div class="ui-resizable-handle ui-resizable-n" style="z-index: 90;"></div></div>






<script type="text/javascript">
    sys_info = {"notebook_version": "5.6.0", "notebook_path": "C:\\Users\\Stevy\\Anaconda3\\lib\\site-packages\\notebook", "commit_source": "", "commit_hash": "", "sys_version": "3.7.0 (default, Jun 28 2018, 08:04:48) [MSC v.1912 64 bit (AMD64)]", "sys_executable": "C:\\Users\\Stevy\\Anaconda3\\python.exe", "sys_platform": "win32", "platform": "Windows-10-10.0.17134-SP0", "os_name": "nt", "default_encoding": "utf-8"};
</script>

<script src="./README_files/encoding.js.download" charset="utf-8"></script>

<script src="./README_files/main.min.js.download" type="text/javascript" charset="utf-8"></script>



<script type="text/javascript">
  function _remove_token_from_url() {
    if (window.location.search.length <= 1) {
      return;
    }
    var search_parameters = window.location.search.slice(1).split('&');
    for (var i = 0; i < search_parameters.length; i++) {
      if (search_parameters[i].split('=')[0] === 'token') {
        // remote token from search parameters
        search_parameters.splice(i, 1);
        var new_search = '';
        if (search_parameters.length) {
          new_search = '?' + search_parameters.join('&');
        }
        var new_url = window.location.origin + 
                      window.location.pathname + 
                      new_search + 
                      window.location.hash;
        window.history.replaceState({}, "", new_url);
        return;
      }
    }
  }
  _remove_token_from_url();
</script>


<div style="position: absolute; width: 0px; height: 0px; overflow: hidden; padding: 0px; border: 0px; margin: 0px;"><div id="MathJax_Font_Test" style="position: absolute; visibility: hidden; top: 0px; left: 0px; width: auto; min-width: 0px; max-width: none; padding: 0px; border: 0px; margin: 0px; white-space: nowrap; text-align: left; text-indent: 0px; text-transform: none; line-height: normal; letter-spacing: normal; word-spacing: normal; font-size: 40px; font-weight: normal; font-style: normal; font-family: STIXMathJax_Main, sans-serif;"></div></div><div id="varInspector-wrapper" class="ui-draggable ui-resizable varInspector-float-wrapper" style="position: fixed; display: none; max-height: 719px;"><div id="varInspector-header" class="header">Variable Inspector <a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="kill-btn" title="Close window">[x]</a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="hide-btn" title="Hide Variable Inspector">[-]</a><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" class="reload-btn" title="Reload Variable Inspector">  ↻</a><span>&nbsp;&nbsp;</span><span>&nbsp;&nbsp;</span></div><div id="varInspector" class="varInspector" style="height: 92.222px; max-height: 699px;"><div class="inspector"><table class="table fixed table-condensed table-nonfluid tablesorter tablesorter-default" role="grid"><colgroup><col>  <col><col></colgroup><thead><tr role="row" class="tablesorter-headerRow"><th data-column="0" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="X: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">X</div></th><th data-column="1" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Name: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Name</div></th><th data-column="2" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Type: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Type</div></th><th data-column="3" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Size: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Size</div></th><th data-column="4" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Shape: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Shape</div></th><th data-column="5" class="tablesorter-header tablesorter-headerUnSorted" tabindex="0" scope="col" role="columnheader" aria-disabled="false" unselectable="on" aria-sort="none" aria-label="Value: No sort applied, activate to apply an ascending sort" style="user-select: none;"><div class="tablesorter-header-inner">Value</div></th></tr></thead><tbody aria-live="polite" aria-relevant="all"><tr role="row"><td>  </td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del ax1&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>ax1</td><td>AxesSubplot</td><td>56</td><td></td><td>AxesSubplot(0.125,0.125;0.352273x0.755)</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del ax2&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>ax2</td><td>AxesSubplot</td><td>56</td><td></td><td>AxesSubplot(0.547727,0.125;0.352273x0...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del centers&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>centers</td><td>ndarray</td><td>168</td><td>(3, 7)</td><td>[[18.72180328 16.29737705  0.88508689...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del df&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>df</td><td>DataFrame</td><td>14360</td><td>(210, 9)</td><td>         A      P       C     LK     ...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del fig&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>fig</td><td>Figure</td><td>56</td><td></td><td>Figure(720x432)</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del g&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>g</td><td>FacetGrid</td><td>56</td><td></td><td><seaborn.axisgrid.facetgrid object="" at...<="" td=""></seaborn.axisgrid.facetgrid></td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del k&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>k</td><td>int</td><td>28</td><td></td><td>9</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del kmeans&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>kmeans</td><td>KMeans</td><td>56</td><td></td><td>KMeans(algorithm='auto', copy_x=True,...</td></tr><tr role="row"><td><a href="http://localhost:8888/notebooks/Documents/Course-Material/Course_Material/S_15_K_Means_Clust/Varieties_of_the_wheat_seed_dataset.ipynb#" onclick="Jupyter.notebook.kernel.execute(&#39;del sum_square&#39;); Jupyter.notebook.events.trigger(&#39;varRefresh&#39;); ">x</a></td><td>sum_square</td><td>dict</td><td>368</td><td></td><td>{1: 2852.276219701762, 2: 1090.727229...</td></tr></tbody></table></div></div><div class="ui-resizable-handle ui-resizable-e" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-s" style="z-index: 90;"></div><div class="ui-resizable-handle ui-resizable-se ui-icon ui-icon-gripsmall-diagonal-se" style="z-index: 90;"></div></div><style>#toc li > span:hover { background-color: #DAA520 }
.toc-item-highlight-select  {background-color: #FFD700}
.toc-item-highlight-execute  {background-color: #FF0000}
.toc-item-highlight-execute.toc-item-highlight-select   {background-color: #FFD700}div#menubar-container, div#header-container {
width: auto;
padding-left: 20px; }#toc-wrapper { background-color: #FFFFFF}
#toc a, #navigate_menu a, .toc { color: #333333}#toc-wrapper .toc-item-num { color: #000000}.sidebar-wrapper { border-color: #EEEEEE}.highlight_on_scroll { border-left: solid 4px #2447f0}</style><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 1</strong>  <div title="jupyter-notebook:change-cell-to-heading-1" class="pull-right command-shortcut"><kbd>1</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i>automatically indent selection  <div title="jupyter-notebook:auto-indent" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="1"><i class="fa fa-icon {{icon}}"></i>change cell to code  <div title="jupyter-notebook:change-cell-to-code" class="pull-right command-shortcut"><kbd>Y</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="2"><i class="fa fa-icon {{icon}}"></i>change cell to heading 1  <div title="jupyter-notebook:change-cell-to-heading-1" class="pull-right command-shortcut"><kbd>1</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="3"><i class="fa fa-icon {{icon}}"></i>change cell to heading 2  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="4"><i class="fa fa-icon {{icon}}"></i>change cell to heading 3  <div title="jupyter-notebook:change-cell-to-heading-3" class="pull-right command-shortcut"><kbd>3</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="5"><i class="fa fa-icon {{icon}}"></i>change cell to heading 4  <div title="jupyter-notebook:change-cell-to-heading-4" class="pull-right command-shortcut"><kbd>4</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="6"><i class="fa fa-icon {{icon}}"></i>change cell to heading 5  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="7"><i class="fa fa-icon {{icon}}"></i>change cell to heading 6  <div title="jupyter-notebook:change-cell-to-heading-6" class="pull-right command-shortcut"><kbd>6</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="8"><i class="fa fa-icon {{icon}}"></i>change cell to markdown  <div title="jupyter-notebook:change-cell-to-markdown" class="pull-right command-shortcut"><kbd>M</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="9"><i class="fa fa-icon {{icon}}"></i>change cell to raw  <div title="jupyter-notebook:change-cell-to-raw" class="pull-right command-shortcut"><kbd>R</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="10"><i class="fa fa-icon {{icon}}"></i>clear all cells output  <div title="jupyter-notebook:clear-all-cells-output" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class=""><a href="javascript:;" data-group="jupyter-notebook" data-index="11"><i class="fa fa-icon {{icon}}"></i>clear cell output  <div title="jupyter-notebook:clear-cell-output" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class=""><a href="javascript:;" data-group="jupyter-notebook" data-index="12"><i class="fa fa-icon {{icon}}"></i>close the pager  <div title="jupyter-notebook:close-pager" class="pull-right command-shortcut"><kbd>Esc</kbd></div></a></li><li class=""><a href="javascript:;" data-group="jupyter-notebook" data-index="15"><i class="fa fa-icon fa-repeat"></i>confirm restart kernel  <div title="jupyter-notebook:confirm-restart-kernel" class="pull-right command-shortcut"><kbd>0</kbd>,<kbd>0</kbd></div></a></li><li class=""><a href="javascript:;" data-group="jupyter-notebook" data-index="16"><i class="fa fa-icon {{icon}}"></i>confirm restart kernel and clear output  <div title="jupyter-notebook:confirm-restart-kernel-and-clear-output" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class=""><a href="javascript:;" data-group="jupyter-notebook" data-index="17"><i class="fa fa-icon fa-forward"></i>confirm restart kernel and run all cells  <div title="jupyter-notebook:confirm-restart-kernel-and-run-all-cells" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class=""><a href="javascript:;" data-group="jupyter-notebook" data-index="18"><i class="fa fa-icon fa-repeat"></i>confirm shutdown kernel  <div title="jupyter-notebook:confirm-shutdown-kernel" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class=""><a href="javascript:;" data-group="jupyter-notebook" data-index="19"><i class="fa fa-icon {{icon}}"></i>copy cell attachments  <div title="jupyter-notebook:copy-cell-attachments" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="20"><i class="fa fa-icon fa-copy"></i>copy selected cells  <div title="jupyter-notebook:copy-cell" class="pull-right command-shortcut"><kbd>C</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="22"><i class="fa fa-icon {{icon}}"></i>cut cell attachments  <div title="jupyter-notebook:cut-cell-attachments" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="23"><i class="fa fa-icon fa-cut"></i>cut selected cells  <div title="jupyter-notebook:cut-cell" class="pull-right command-shortcut"><kbd>X</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="25"><i class="fa fa-icon {{icon}}"></i>delete cells  <div title="jupyter-notebook:delete-cell" class="pull-right command-shortcut"><kbd>D</kbd>,<kbd>D</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="26"><i class="fa fa-icon {{icon}}"></i>duplicate notebook  <div title="jupyter-notebook:duplicate-notebook" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="27"><i class="fa fa-icon {{icon}}"></i>edit command mode keyboard shortcuts  <div title="jupyter-notebook:edit-command-mode-keyboard-shortcuts" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="29"><i class="fa fa-icon {{icon}}"></i>enter command mode  <div title="jupyter-notebook:enter-command-mode" class="pull-right edit-shortcut"><kbd>Esc</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="30"><i class="fa fa-icon {{icon}}"></i>enter edit mode  <div title="jupyter-notebook:enter-edit-mode" class="pull-right command-shortcut"><kbd>Enter</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="31"><i class="fa fa-icon {{icon}}"></i>extend selection above  <div title="jupyter-notebook:extend-selection-above" class="pull-right command-shortcut"><kbd>Shift-K</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="32"><i class="fa fa-icon {{icon}}"></i>extend selection below  <div title="jupyter-notebook:extend-selection-below" class="pull-right command-shortcut"><kbd>Shift-J</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="33"><i class="fa fa-icon {{icon}}"></i>find and replace  <div title="jupyter-notebook:find-and-replace" class="pull-right command-shortcut"><kbd>F</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="34"><i class="fa fa-icon {{icon}}"></i>hide all line numbers  <div title="jupyter-notebook:hide-all-line-numbers" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="35"><i class="fa fa-icon {{icon}}"></i>hide menubar  <div title="jupyter-notebook:hide-menubar" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="36"><i class="fa fa-icon {{icon}}"></i>hide the header  <div title="jupyter-notebook:hide-header" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="37"><i class="fa fa-icon {{icon}}"></i>hide the toolbar  <div title="jupyter-notebook:hide-toolbar" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="38"><i class="fa fa-icon {{icon}}"></i>ignore  <div title="jupyter-notebook:ignore" class="pull-right command-shortcut"><kbd>Shift</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="40"><i class="fa fa-icon {{icon}}"></i>insert cell above  <div title="jupyter-notebook:insert-cell-above" class="pull-right command-shortcut"><kbd>A</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="41"><i class="fa fa-icon fa-plus"></i>insert cell below  <div title="jupyter-notebook:insert-cell-below" class="pull-right command-shortcut"><kbd>B</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="42"><i class="fa fa-icon {{icon}}"></i>insert image  <div title="jupyter-notebook:insert-image" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="45"><i class="fa fa-icon fa-stop"></i>interrupt the kernel  <div title="jupyter-notebook:interrupt-kernel" class="pull-right command-shortcut"><kbd>I</kbd>,<kbd>I</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="46"><i class="fa fa-icon {{icon}}"></i>merge cell with next cell  <div title="jupyter-notebook:merge-cell-with-next-cell" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="47"><i class="fa fa-icon {{icon}}"></i>merge cell with previous cell  <div title="jupyter-notebook:merge-cell-with-previous-cell" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="48"><i class="fa fa-icon {{icon}}"></i>merge cells  <div title="jupyter-notebook:merge-cells" class="pull-right command-shortcut"><kbd>Shift-M</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="49"><i class="fa fa-icon {{icon}}"></i>merge selected cells  <div title="jupyter-notebook:merge-selected-cells" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="50"><i class="fa fa-icon fa-arrow-down"></i>move cells down  <div title="jupyter-notebook:move-cell-down" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="51"><i class="fa fa-icon fa-arrow-up"></i>move cells up  <div title="jupyter-notebook:move-cell-up" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="52"><i class="fa fa-icon {{icon}}"></i>move cursor down  <div title="jupyter-notebook:move-cursor-down" class="pull-right edit-shortcut"><kbd>Down</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="53"><i class="fa fa-icon {{icon}}"></i>move cursor up  <div title="jupyter-notebook:move-cursor-up" class="pull-right edit-shortcut"><kbd>Up</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="54"><i class="fa fa-icon {{icon}}"></i>paste cell attachments  <div title="jupyter-notebook:paste-cell-attachments" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="55"><i class="fa fa-icon {{icon}}"></i>paste cell replace  <div title="jupyter-notebook:paste-cell-replace" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="56"><i class="fa fa-icon {{icon}}"></i>paste cells above  <div title="jupyter-notebook:paste-cell-above" class="pull-right command-shortcut"><kbd>Shift-V</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="57"><i class="fa fa-icon fa-paste"></i>paste cells below  <div title="jupyter-notebook:paste-cell-below" class="pull-right command-shortcut"><kbd>V</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="62"><i class="fa fa-icon {{icon}}"></i>rename notebook  <div title="jupyter-notebook:rename-notebook" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="63"><i class="fa fa-icon {{icon}}"></i>restart kernel  <div title="jupyter-notebook:restart-kernel" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="64"><i class="fa fa-icon {{icon}}"></i>restart kernel and clear output  <div title="jupyter-notebook:restart-kernel-and-clear-output" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="65"><i class="fa fa-icon {{icon}}"></i>restart kernel and run all cells  <div title="jupyter-notebook:restart-kernel-and-run-all-cells" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="66"><i class="fa fa-icon {{icon}}"></i>run all cells  <div title="jupyter-notebook:run-all-cells" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="67"><i class="fa fa-icon {{icon}}"></i>run all cells above  <div title="jupyter-notebook:run-all-cells-above" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="68"><i class="fa fa-icon {{icon}}"></i>run all cells below  <div title="jupyter-notebook:run-all-cells-below" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="69"><i class="fa fa-icon {{icon}}"></i>run cell and insert below  <div title="jupyter-notebook:run-cell-and-insert-below" class="pull-right command-shortcut"><kbd>Alt-Enter</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="70"><i class="fa fa-icon fa-step-forward"></i>run cell and select next  <div title="jupyter-notebook:run-cell-and-select-next" class="pull-right command-shortcut"><kbd>Shift-Enter</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="71"><i class="fa fa-icon {{icon}}"></i>run selected cells  <div title="jupyter-notebook:run-cell" class="pull-right command-shortcut"><kbd>Ctrl-Enter</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="73"><i class="fa fa-icon fa-save"></i>save notebook  <div title="jupyter-notebook:save-notebook" class="pull-right command-shortcut"><kbd>Ctrl-S</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="76"><i class="fa fa-icon {{icon}}"></i>scroll cell center  <div title="jupyter-notebook:scroll-cell-center" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="77"><i class="fa fa-icon {{icon}}"></i>scroll cell top  <div title="jupyter-notebook:scroll-cell-top" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="78"><i class="fa fa-icon {{icon}}"></i>scroll notebook down  <div title="jupyter-notebook:scroll-notebook-down" class="pull-right command-shortcut"><kbd>Space</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="79"><i class="fa fa-icon {{icon}}"></i>scroll notebook up  <div title="jupyter-notebook:scroll-notebook-up" class="pull-right command-shortcut"><kbd>Shift-Space</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="80"><i class="fa fa-icon {{icon}}"></i>select next cell  <div title="jupyter-notebook:select-next-cell" class="pull-right command-shortcut"><kbd>Down</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="81"><i class="fa fa-icon {{icon}}"></i>select previous cell  <div title="jupyter-notebook:select-previous-cell" class="pull-right command-shortcut"><kbd>Up</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="83"><i class="fa fa-icon {{icon}}"></i>show all line numbers  <div title="jupyter-notebook:show-all-line-numbers" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="84"><i class="fa fa-icon fa-keyboard-o"></i>show command pallette  <div title="jupyter-notebook:show-command-palette" class="pull-right command-shortcut"><kbd>Ctrl-Shift-P</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="85"><i class="fa fa-icon {{icon}}"></i>show keyboard shortcuts  <div title="jupyter-notebook:show-keyboard-shortcuts" class="pull-right command-shortcut"><kbd>H</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="86"><i class="fa fa-icon {{icon}}"></i>show menubar  <div title="jupyter-notebook:show-menubar" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="87"><i class="fa fa-icon {{icon}}"></i>show the header  <div title="jupyter-notebook:show-header" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="88"><i class="fa fa-icon {{icon}}"></i>show the toolbar  <div title="jupyter-notebook:show-toolbar" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="89"><i class="fa fa-icon {{icon}}"></i>shutdown kernel  <div title="jupyter-notebook:shutdown-kernel" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="90"><i class="fa fa-icon {{icon}}"></i>shutdown kernel and close window  <div title="jupyter-notebook:close-and-halt" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="91"><i class="fa fa-icon {{icon}}"></i>split cell at cursor  <div title="jupyter-notebook:split-cell-at-cursor" class="pull-right edit-shortcut"><kbd>Ctrl-Shift-Minus</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="92"><i class="fa fa-icon {{icon}}"></i>toggle all cells output collapsed  <div title="jupyter-notebook:toggle-all-cells-output-collapsed" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="93"><i class="fa fa-icon {{icon}}"></i>toggle all cells output scrolled  <div title="jupyter-notebook:toggle-all-cells-output-scrolled" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="94"><i class="fa fa-icon fa-list-ol"></i>toggle all line numbers  <div title="jupyter-notebook:toggle-all-line-numbers" class="pull-right command-shortcut"><kbd>Shift-L</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="95"><i class="fa fa-icon {{icon}}"></i>toggle cell output  <div title="jupyter-notebook:toggle-cell-output-collapsed" class="pull-right command-shortcut"><kbd>O</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="96"><i class="fa fa-icon {{icon}}"></i>toggle cell scrolling  <div title="jupyter-notebook:toggle-cell-output-scrolled" class="pull-right command-shortcut"><kbd>Shift-O</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="98"><i class="fa fa-icon {{icon}}"></i>toggle header  <div title="jupyter-notebook:toggle-header" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="99"><i class="fa fa-icon {{icon}}"></i>toggle line numbers  <div title="jupyter-notebook:toggle-cell-line-numbers" class="pull-right command-shortcut"><kbd>L</kbd></div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="100"><i class="fa fa-icon {{icon}}"></i>toggle menubar  <div title="jupyter-notebook:toggle-menubar" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="101"><i class="fa fa-icon {{icon}}"></i>toggle rtl layout  <div title="jupyter-notebook:toggle-rtl-layout" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="103"><i class="fa fa-icon {{icon}}"></i>toggle toolbar  <div title="jupyter-notebook:toggle-toolbar" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="107"><i class="fa fa-icon {{icon}}"></i>trust notebook  <div title="jupyter-notebook:trust-notebook" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="jupyter-notebook" data-index="110"><i class="fa fa-icon {{icon}}"></i>undo cell deletion  <div title="jupyter-notebook:undo-cell-deletion" class="pull-right command-shortcut"><kbd>Z</kbd></div></a></li><li class="typeahead-group" data-search-group="collapsible_headings"><a href="javascript:;">collapsible_headings command group</a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="13"><i class="fa fa-icon fa-caret-right"></i>collapse-all-headings  <div title="collapsible_headings:collapse_all_headings" class="pull-right command-shortcut"><kbd>Ctrl-Shift-Left</kbd></div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="14"><i class="fa fa-icon fa-caret-right"></i>collapse-heading  <div title="collapsible_headings:collapse_heading" class="pull-right command-shortcut"><kbd>Left</kbd></div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="43"><i class="fa fa-icon fa-caret-up"></i>insert-heading-above  <div title="collapsible_headings:insert_heading_above" class="pull-right command-shortcut"><kbd>Shift-A</kbd></div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="44"><i class="fa fa-icon fa-caret-down"></i>insert-heading-below  <div title="collapsible_headings:insert_heading_below" class="pull-right command-shortcut"><kbd>Shift-B</kbd></div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="82"><i class="fa fa-icon {{icon}}"></i>select-heading-section  <div title="collapsible_headings:select_heading_section" class="pull-right command-shortcut"><kbd>Shift-Right</kbd></div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="105"><i class="fa fa-icon fa-angle-double-up"></i>toggle-collapse-all-headings  <div title="collapsible_headings:toggle_collapse_all_headings" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="106"><i class="fa fa-icon fa-angle-double-up"></i>toggle-collapse-heading  <div title="collapsible_headings:toggle_collapse_heading" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="108"><i class="fa fa-icon fa-caret-down"></i>uncollapse-all-headings  <div title="collapsible_headings:uncollapse_all_headings" class="pull-right command-shortcut"><kbd>Ctrl-Shift-Right</kbd></div></a></li><li><a href="javascript:;" data-group="collapsible_headings" data-index="109"><i class="fa fa-icon fa-caret-down"></i>uncollapse-heading  <div title="collapsible_headings:uncollapse_heading" class="pull-right command-shortcut"><kbd>Right</kbd></div></a></li><li class="typeahead-group" data-search-group="gist_it"><a href="javascript:;">gist_it command group</a></li><li><a href="javascript:;" data-group="gist_it" data-index="21"><i class="fa fa-icon fa-github"></i>create gist from notebook  <div title="gist_it:create-gist-from-notebook" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class="typeahead-group" data-search-group="code_font_size"><a href="javascript:;">code_font_size command group</a></li><li><a href="javascript:;" data-group="code_font_size" data-index="24"><i class="fa fa-icon fa-search-minus"></i>decrease code font size  <div title="code_font_size:decrease-code-font-size" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="code_font_size" data-index="39"><i class="fa fa-icon fa-search-plus"></i>increase code font size  <div title="code_font_size:increase-code-font-size" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class="typeahead-group" data-search-group="widgets"><a href="javascript:;">widgets command group</a></li><li><a href="javascript:;" data-group="widgets" data-index="28"><i class="fa fa-icon fa-sliders"></i>embed interactive widgets  <div title="widgets:embed-interactive-widgets" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="widgets" data-index="72"><i class="fa fa-icon fa-truck"></i>save clear widgets  <div title="widgets:save-clear-widgets" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="widgets" data-index="74"><i class="fa fa-icon fa-sliders"></i>save widget state  <div title="widgets:save-widget-state" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="widgets" data-index="75"><i class="fa fa-icon fa-truck"></i>save with widgets  <div title="widgets:save-with-widgets" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class="typeahead-group" data-search-group="code_prettify"><a href="javascript:;">code_prettify command group</a></li><li><a href="javascript:;" data-group="code_prettify" data-index="58"><i class="fa fa-icon fa-legal"></i>process-all-cells  <div title="code_prettify:process_all_cells" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li><a href="javascript:;" data-group="code_prettify" data-index="60"><i class="fa fa-icon fa-legal"></i>process-selected-cells  <div title="code_prettify:process_selected_cells" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class="typeahead-group" data-search-group="autopep8"><a href="javascript:;">autopep8 command group</a></li><li><a href="javascript:;" data-group="autopep8" data-index="59"><i class="fa fa-icon fa-legal"></i>process-all-cells  <div title="autopep8:process_all_cells" class="pull-right command-shortcut"><kbd>Ctrl-Shift-L</kbd></div></a></li><li><a href="javascript:;" data-group="autopep8" data-index="61"><i class="fa fa-icon fa-legal"></i>process-selected-cells  <div title="autopep8:process_selected_cells" class="pull-right command-shortcut"><kbd>Ctrl-L</kbd></div></a></li><li class="typeahead-group" data-search-group="auto"><a href="javascript:;">auto command group</a></li><li><a href="javascript:;" data-group="auto" data-index="97"><i class="fa fa-icon fa-comment-o"></i>toggle codefolding  <div title="auto:toggle-codefolding" class="pull-right command-shortcut"><kbd>Alt-F</kbd></div></a></li><li class="typeahead-group" data-search-group="toc2"><a href="javascript:;">toc2 command group</a></li><li><a href="javascript:;" data-group="toc2" data-index="102"><i class="fa fa-icon fa-list"></i>toggle toc  <div title="toc2:toggle-toc" class="pull-right no-shortcut">{{shortcut}}</div></a></li><li class="typeahead-group" data-search-group="varInspector"><a href="javascript:;">varInspector command group</a></li><li><a href="javascript:;" data-group="varInspector" data-index="104"><i class="fa fa-icon fa-crosshairs"></i>toggle variable inspector  <div title="varInspector:toggle-variable-inspector" class="pull-right no-shortcut">{{shortcut}}</div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 1</strong>  <div title="jupyter-notebook:change-cell-to-heading-1" class="pull-right command-shortcut"><kbd>1</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 2</strong>  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 2</strong>  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 2</strong>  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 2</strong>  <div title="jupyter-notebook:change-cell-to-heading-2" class="pull-right command-shortcut"><kbd>2</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div><div class="modal cmd-palette" style="display: none;"><div class="modal-dialog"><div class="modal-content"><div class="modal-body"><form><div class="typeahead-container"><div class="typeahead-field"><span class="typeahead-query" style="position: relative;"><input type="search"><input type="search" readonly="readonly" unselectable="on" tabindex="-1" class="typeahead-hint" style="border-color: transparent; position: absolute; top: 0px; display: inline; z-index: -1; float: none; color: rgb(192, 192, 192); box-shadow: none; cursor: default; user-select: none;"></span><span class="typeahead-button"><button type="submit"><span class="typeahead-search-icon"></span></button></span></div><div class="typeahead-result"><ul class="typeahead-list"><li class="typeahead-group" data-search-group="jupyter-notebook"><a href="javascript:;">jupyter-notebook command group</a></li><li class="active"><a href="javascript:;" data-group="jupyter-notebook" data-index="0"><i class="fa fa-icon {{icon}}"></i><strong>change cell to heading 5</strong>  <div title="jupyter-notebook:change-cell-to-heading-5" class="pull-right command-shortcut"><kbd>5</kbd></div></a></li></ul></div></div></form></div></div></div></div></body></html>