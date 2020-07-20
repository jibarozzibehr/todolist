<script>
	import { onMount } from 'svelte';
	let date = new Date();
	$: hour = (date.getHours() < 10) ? '0' + date.getHours() : date.getHours();
	$: min = (date.getMinutes() < 10) ? '0' + date.getMinutes() : date.getMinutes();
	$: sec = (date.getSeconds() < 10) ? '0' + date.getSeconds() : date.getSeconds();
	let dayOrNight = 'AM';
	
	
	onMount( () => {
		const interval = setInterval(() => {
			date = new Date();
			dayOrNight = (hour >= 12) ? "PM" : "AM";
		}, 1000);
    });
</script>


<svelte:head>
    <link href="https://fonts.googleapis.com/css2?family=Ranchers&display=swap" rel="stylesheet"> 
    <style type="text/css">

        /* @group Blink */
        .blink {
            -webkit-animation: blink 1s linear infinite;
            -moz-animation: blink 1s linear infinite;
            -ms-animation: blink 1s linear infinite;
            -o-animation: blink 1s linear infinite;
            animation: blink 1s linear infinite;
        }
        @-webkit-keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 1; }
            50.01% { opacity: 0; }
            100% { opacity: 0; }
        }
        @-moz-keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 1; }
            50.01% { opacity: 0; }
            100% { opacity: 0; }
        }
        @-ms-keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 1; }
            50.01% { opacity: 0; }
            100% { opacity: 0; }
        }
        @-o-keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 1; }
            50.01% { opacity: 0; }
            100% { opacity: 0; }
        }
        @keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 1; }
            50.01% { opacity: 0; }
            100% { opacity: 0; }
        }
        /* @end */
    </style>
</svelte:head>

<style>
    @import 'fuentes.css';

    @font-face {
        font-family: 'Digital Dismay';
        font-style: normal;
        /*font-weight: 400;*/
        src: url('/fonts/Digital Dismay.otf');
        unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
    }

	.clockWrapper, .clockDisplay {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	
	.clockWrapper {
		/*width: 75%;
		height: 50%;
		border-radius: 15px;
		background: #ffffff;*/
		width: 200px;
        height: 80px;
        margin: 0 auto;
        margin-top: 20px;
        background: linear-gradient(130deg, rgba(125,140,115,1) 0%, rgba(88,98,82,1) 100%);
        
        border-radius: 5px;
        text-align: center;
        vertical-align: middle;
        line-height: 70px; /*div height - border size*/
        /*font-size: 25px;
            font-weight: 900;*/
        border: 10px;
        border-style: solid;
        /*border-color: #EFEEEE;*/

        /*-webkit-box-shadow: 6px 6px 16px 0px rgba(209,205,199,0.5);
        -moz-box-shadow: 6px 6px 16px 0px rgba(209,205,199,0.5);*/
        border-color: #dde9f7;
        box-shadow: 6px 6px 11px #bcc6d2, 
                    -6px -6px 11px #feffff,
                    inset 1px 1px 2px 0px rgba(0,0,0,0.5);
        

        position: relative;

        transition: border-color 0.3s, box-shadow 0.3s, background 0.3s;
	}
	.clockDisplay { /*Numeros hora*/
		width: 99%;
		height: 99%;
		font-size: 2.5em;
		/*background: #059506;*/
		/*border-radius: 15px;*/
		color: rgb(53, 53, 53);
        font-family: 'Digital Dismay';
        position: absolute;
        color:rgb(53, 53, 53);

        transition: color 0.3s
    }
    
    .clockDisplay2 { /*Numeros de atrás*/
		width: 99%;
		height: 99%;
		font-size: 2.5em;
		/*background: #059506;*/
		/*border-radius: 15px;*/
        color: rgba(53, 53, 53);
        opacity: 0.3;
        font-family: 'Digital Dismay';
        position: absolute;
        color:rgb(53, 53, 53);
        margin-bottom: 10px;
	}

    :global(body.dark-mode) .clockWrapper {
        border-color: #1A1A1A;
        box-shadow: 6px 6px 12px #121212, 
                    -6px -6px 12px #2A2A2A;
        
        /*background: linear-gradient(90deg, rgba(199,255,231,1) 0%, rgba(89,252,183,1) 11%, rgba(61,187,129,1) 50%, rgba(47,143,99,1) 100%);*/
        background: linear-gradient(90deg, rgba(183,255,224,1) 0%, rgba(89,252,183,1) 5%, rgba(61,187,129,1) 50%, rgba(47,143,99,1) 100%);
    }

    :global(body.dark-mode) .clockDisplay {
        color: #013622;
    }
</style>


<div>
	<div id='' class='clockWrapper'>
		<div class='clockDisplay'> 
			{hour}<p class="tab blink">:</p>{min}<p class="tab blink">:</p>{sec}
		</div>
        <div class="clockDisplay2">88:88:88</div>
    </div>
</div>