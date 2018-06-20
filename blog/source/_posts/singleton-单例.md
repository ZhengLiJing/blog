---
title: singleton 单例
date: 2018-06-20 20:47:17
tags: javascript设计模式
categories: javascript
---
JavaScript设计模式之单例
# 单例模式

    const Singleton = (function() {

        var instantiated;
        function init() {
            return {
                publicMethod: function () {
                    console.log('something');
                },
                publicVar: 'privateVar';
            }
        },

        return {
            getInstance: function () {
                if(instantiated === undefined) {
                    instantiated = init();
                }
                return instancitated;
            }
        }
    })()