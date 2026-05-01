# Typeracer.com---cheat

# Right click on the page 
# Click inspect
# Click on the Console tab
# Paste the code inside the Console
# Hold space 
# Site detects the WPM above 100 and asks you to do a captcha test.


(function () {
    function run($) {
        let inputText = "";
        let i = 0;

        // remove any previous broken handlers
        $('body').off('keypress', '.txtInput');

        $('body').on('keypress', '.txtInput', function (e) {

            // get text once
            if (!inputText) {
                inputText = $('.inputPanel tr:first').text().trim();
                console.log("Text:", inputText);
            }

            // stop at end
            if (i >= inputText.length) {
                e.preventDefault();
                return;
            }

            const char = inputText.charAt(i);

            // safety check (prevents "undefined")
            if (!char) {
                i++;
                e.preventDefault();
                return;
            }

            if (char === " ") {
                if ((e.which || e.keyCode) === 32) {
                    i++;
                } else {
                    e.preventDefault();
                }
            } else {
                e.preventDefault();
                $(this).val($(this).val() + char);
                i++;
            }
        });
    }

    // load jQuery if needed
    if (typeof jQuery === "undefined") {
        const script = document.createElement("script");
        script.src = "https://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js";
        script.onload = function () {
            run(jQuery.noConflict());
        };
        document.head.appendChild(script);
    } else {
        run(jQuery);
    }

})();
