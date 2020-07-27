# cotizarmicarga<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Envío de formulario por WhatsApp</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js" charset="utf-8"></script>
    <!-- <link rel="stylesheet" href="style.css"> -->

    <style>
        *{
        margin: 0;
        padding: 0;
        text-decoration: none;
        font-family: "Montserrat", sans-serif;
    }

    body{
        min-height: 100vh;
        background-image: linear-gradient(120deg, #3498db, #8e44ad);
    }

    .formulario{
        width: 360px;
        background: #f1f1f1;
        height: 400px;
        padding: 80px 40px;
        border-radius: 10px;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        box-shadow: 2px 2px 10px 5px rgba(0, 0, 0, 0.2);
    }

    .formulario h1{
        text-align: center;
        margin-bottom: 60px;
        color: #333;
        font-weight: 600;
    }

    .box-input{
        border-bottom: 2px solid #adadad;
        position: relative;
        margin: 30px 0;
    }

    .box-input input{
        font-size: 16px;
        color: #333;
        border: none;
        width: 100%;
        outline: none;
        background: none;
        padding: 0 5px;
        height: 40px;
    }

    .box-input span::before{
        content: attr(data-placeholder);
        position: absolute;
        top: 50%;
        left: 5px;
        color: #adadad;
        transform: translateY(-50%);
        z-index: -1;
        transition: .5s;
    }

    .box-input span::after{
        content: '';
        position: absolute;
        width: 0%;
        height: 2px;
        background: linear-gradient(120deg, #3498db, #8e44ad);
        transition: .5s;
    }

    .focus + span::before{
        top: -5px;
    }

    .focus + span::after{
        width: 100%;
    }

    .boton{
        display: block;
        width: 100%;
        height: 50px;
        background-color: #48bb78;
        border: solid 2px #48bb78;
        color: #fff;
        border-radius: 5px;
        font-weight: 600;
        font-size: 18px;
        box-shadow: 2px 2px 5px 2px rgba(0, 0, 0, 0.1);
    }

    .boton:hover{
        background-color: #2F855A;
        border: solid 2px #2F855A;
        transition: .5s;
    }
    </style>
</head>
<body>

    <form id="formulario" class="formulario">
        <h1>Envío de formulario por WhatsApp</h1>
        <div class="box-input">
            <input name="nombre" id="nombre" type="text" required>
            <span data-placeholder="Escriba su Nombre"></span>
        </div>
        <div class="box-input">
            <input name="apellidos" id="apellidos" type="text" required>
            <span data-placeholder="Escriba sus Apellidos"></span>
        </div>
        <div class="box-input">
            <input name="email" id="email" type="email" required>
            <span data-placeholder="Escriba su Correo Electrónico"></span>
        </div>
        <button id="submit" type="submit" class="boton"><i class="fab fa-whatsapp"></i> Enviar WhatsApp</button>
    </form>

    <script type="text/javascript">
        $(".box-input input").on("focus", function(){
            $(this).addClass("focus");
        });

        $(".box-input input").on("blur", function(){
            if($(this).val() == ""){
                $(this).removeClass("focus");
            }
        });

    </script>

    <script src="https://kit.fontawesome.com/a076d05399.js"></script>
    <!-- <script src="whatsapp.js"></script> -->
</body>
</html>



<script>
    function isMobile() {
        if (sessionStorage.desktop)
            return false;
        else if (localStorage.mobile)
            return true;
        var mobile = ['iphone', 'ipad', 'android', 'blackberry', 'nokia', 'opera mini', 'windows mobile', 'windows phone', 'iemobile'];
        for (var i in mobile)
            if (navigator.userAgent.toLowerCase().indexOf(mobile[i].toLowerCase()) > 0) return true;
        return false;
    }

    const formulario = document.querySelector('#formulario');
    const buttonSubmit = document.querySelector('#submit');
    const urlDesktop = 'https://web.whatsapp.com/';
    const urlMobile = 'whatsapp://';
    const telefono = '51998866670';

    formulario.addEventListener('submit', (event) => {
        event.preventDefault()
        buttonSubmit.innerHTML = '<i class="fas fa-circle-notch fa-spin"></i>'
        buttonSubmit.disabled = true
        setTimeout(() => {
            let nombre = document.querySelector('#nombre').value
            let apellidos = document.querySelector('#apellidos').value
            let email = document.querySelector('#email').value
            let mensaje = 'send?phone=' + telefono + '&text=*_Formulario Easy App CODE_*%0A*¿Cual es tu nombre?*%0A' + nombre + '%0A*¿Cuáles son tus apellidos?*%0A' + apellidos + '%0A*¿Cuál es tu correo electrónico?*%0A' + email + ''
            if(isMobile()) {
                window.open(urlMobile + mensaje, '_blank')
            }else{
                window.open(urlDesktop + mensaje, '_blank')
            }
            buttonSubmit.innerHTML = '<i class="fab fa-whatsapp"></i> Enviar WhatsApp'
            buttonSubmit.disabled = false
        }, 3000);
    });    
</script>
