# observer

## jquery下观察者模式的使用
### 使用trigger()方法
<script src="Scripts/jquery-2.1.1.min.js"></script>
    <script type="text/javascript">
        $(function() {
            $('body').on('someclick', function () {
                console.log('被点击了~~');
            });
            $('body').trigger('someclick');
        });      
    </script> 
### 代码中.on("someclick"),即是发布了someclick事件，trigger("someclick")进行订阅 <br />
### 于是我们可以这样做，为jQuery观察者模式专门写一个扩展方法。
    (function($) {
                var o = $({});//自定义事件对象
                $.each({
                    trigger: 'publish',
                    on: 'subscribe',
                    off: 'unsubscribe'
                }, function(key, val) {
                    jQuery[val] = function() {
                        o[key].apply(o, arguments);
                    };
                });
            })(jQuery);


