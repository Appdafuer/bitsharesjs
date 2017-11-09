How to get a compiled bitshares.js for React-Native

1. npm install
2. npm run build
3. ./node_modules/.bin/webpack --config webpack.config.js
4. In the ./build folder there is a bitshares.js.
5. Edit this file and commment out some lines (currently 3957ff):

Before:

```
    /* AMD */ if (true)
        !(__WEBPACK_AMD_DEFINE_ARRAY__ = [__webpack_require__(68)], __WEBPACK_AMD_DEFINE_FACTORY__ = (factory),
				__WEBPACK_AMD_DEFINE_RESULT__ = (typeof __WEBPACK_AMD_DEFINE_FACTORY__ === 'function' ?
				(__WEBPACK_AMD_DEFINE_FACTORY__.apply(exports, __WEBPACK_AMD_DEFINE_ARRAY__)) : __WEBPACK_AMD_DEFINE_FACTORY__),
				__WEBPACK_AMD_DEFINE_RESULT__ !== undefined && (module.exports = __WEBPACK_AMD_DEFINE_RESULT__));
     /* CommonJS */ else if (typeof require === 'function' && typeof module === "object" && module && module["exports"])
         module['exports'] = (function() {
             var Long; try { Long = require("long"); } catch (e) {}
             return factory(Long);
         })();
    /* Global */ else
        (global["dcodeIO"] = global["dcodeIO"] || {})["ByteBuffer"] = factory(global["dcodeIO"]["Long"]);
```

After:

```
            /* AMD */ if (true)
        !(__WEBPACK_AMD_DEFINE_ARRAY__ = [__webpack_require__(68)], __WEBPACK_AMD_DEFINE_FACTORY__ = (factory),
				__WEBPACK_AMD_DEFINE_RESULT__ = (typeof __WEBPACK_AMD_DEFINE_FACTORY__ === 'function' ?
				(__WEBPACK_AMD_DEFINE_FACTORY__.apply(exports, __WEBPACK_AMD_DEFINE_ARRAY__)) : __WEBPACK_AMD_DEFINE_FACTORY__),
				__WEBPACK_AMD_DEFINE_RESULT__ !== undefined && (module.exports = __WEBPACK_AMD_DEFINE_RESULT__));
    // /* CommonJS */ else if (typeof require === 'function' && typeof module === "object" && module && module["exports"])
        // module['exports'] = (function() {
        //     var Long; try { Long = require("long"); } catch (e) {}
        //     return factory(Long);
        // })();
    /* Global */ else
        (global["dcodeIO"] = global["dcodeIO"] || {})["ByteBuffer"] = factory(global["dcodeIO"]["Long"]);

```

Explenation: In the unused CommonJS case (if(true) for AMD), there is a require("Long") which will cause the react-packager to fail.

6. Copy the edited bitshares.js to the BitShares React-Native App.