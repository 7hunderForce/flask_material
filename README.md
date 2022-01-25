 <script type="text/javascript">
        // THEME CHECKER
        var acr_flag = 'none';
        var theme_flag = 'none';
    
        acr_flag = get_cookie('acronym_reader'); 
        app_theme = get_cookie('app_theme');

        if(app_theme == 'dark') {
            $(document.body).addClass('theme-dark');
        }
        if(app_theme == 'light') {
            $(document.body).removeClass('theme-dark');
        }
            


        // SERVICE WORKER
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', function() {
                  navigator.serviceWorker.register("/sw.js")
                  .then(function(registration) {
                      // Registration was successful
                      console.log('ServiceWorker registration successful with scope: ', registration.scope);
                  }, function(err) {
                      // registration failed :(
                      console.log('ServiceWorker registration failed: ', err);
                  });
            });
        } 


        
        // SET COOKIE
        function set_cookie(name,value,days) {
            var expires = "";
            if (days) {
                var date = new Date();
                date.setTime(date.getTime() + (days*24*60*60*1000));
                expires = "; expires=" + date.toUTCString();
            }
            document.cookie = name + "=" + (value || "")  + expires + "; path=/";
        }

        // GET COOKIE
        function get_cookie(name) {
            var nameEQ = name + "=";
            var ca = document.cookie.split(';');
            for(var i=0;i < ca.length;i++) {
                var c = ca[i];
                while (c.charAt(0)==' ') c = c.substring(1,c.length);
                if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length,c.length);
            }
            return null;
        }

        // ERASE COOKIE
        function erase_cookie(name) {   
            document.cookie = name +'=; Path=/; Expires=Thu, 01 Jan 1970 00:00:01 GMT;';
        }

    </script>
  
  
  
  
  # /PWA/
#=========================================================
@app.route('/manifest.json')
def manifest():
    return app.send_from_directory('static', 'manifest.json')

@app.route('/sw.js')
def sw():
    return app.send_static_file('sw.js')
