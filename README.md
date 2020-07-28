# Whatsapp

Integrantes:

Edison S. Jumbo &
Christian Mainato.

*************Explicación del proyecto y sus funcionalidades.**************
La aplicaion llamada ChatApp nos permite interactuar en modo real con otraos usuarios a travez de mensajes de chat
Esta escrito en Java en la plataforma de Android Studio.
Crean y eliminar usuarios
Los usuarios se registran con su correo electronico electronico y su password.
tambien se pueden registrar mediante un numero telefonico, el cual genera un token para su registro 
Permite enviar mensajes de texto en tiempo real
Se puede crear y visualizar grupos
tambien se presenta la lista de contactos
Ademas se puede aceptar o rechasar a un nuevo contacto

 
**************En que API se desarrollo y probó.****************
se probo en la API 16 Android 4.1(Jelly Bean)

**************Debe especificar que modelos de celular, tablet, API fue probado/desarrrollado.*********************
Seprobo en el celular PIXEL XL API 30, Tablet PIXEL C se probo en la API 30 y desarrollo en la Api 16

***************Explicación de lo más importante del código (solo lo relevante).**********************
Lo que mas nos parecio relebante fue la implementacion de los chats para su envio y recepcion, ya que cada uno de ellos,
debieron de estar especificamente identificado con un ID 

private void SendMessage()
    {
        String messageText = MessageInputText.getText().toString();

        if (TextUtils.isEmpty(messageText))
        {
            Toast.makeText(this, "Escriba su primer mensaje...", Toast.LENGTH_SHORT).show();
        }
        else
        {
            String messageSenderRef = "Messages/" + messageSenderID + "/" + messageReceiverID;
            String messageReceiverRef = "Messages/" + messageReceiverID + "/" + messageSenderID;

            DatabaseReference userMessageKeyRef = RootRef.child("Messages")
                    .child(messageSenderID).child(messageReceiverID).push();

            String messagePushID = userMessageKeyRef.getKey();

            Map messageTextBody = new HashMap();
            messageTextBody.put("message", messageText);
            messageTextBody.put("type", "text");
            messageTextBody.put("from", messageSenderID);
            messageTextBody.put("to", messageReceiverID);
            messageTextBody.put("messageID", messagePushID);
            messageTextBody.put("time", saveCurrentTime);
            messageTextBody.put("date", saveCurrentDate);

            Map messageBodyDetails = new HashMap();
            messageBodyDetails.put(messageSenderRef + "/" + messagePushID, messageTextBody);
            messageBodyDetails.put( messageReceiverRef + "/" + messagePushID, messageTextBody);

            RootRef.updateChildren(messageBodyDetails).addOnCompleteListener(new OnCompleteListener() {
                @Override
                public void onComplete(@NonNull Task task)
                {
                    if (task.isSuccessful())
                    {
                        Toast.makeText(ChatActivity.this, "Mensaje Enviado...", Toast.LENGTH_SHORT).show();
                    }
                    else
                    {
                        Toast.makeText(ChatActivity.this, "Error", Toast.LENGTH_SHORT).show();
                    }
                    MessageInputText.setText("");
                }
            });
        }
    }

*********************Manual de uso.*************************

********  Manual de Uso ********
ChatApp

1) Opciones de ingreso.

*** Correo & Contraseña.
*** Número Celular con el Token.

2) configuracion del perfil
Ingreso del usuario e informacion.


3) Busqueda de Amigos.

En esta opción se permite enviar un mensaje de confirmación
de solicitud de amistad.
El usuario tiene la opcion de elimar o gregar la peticion de
amistad.

4) Chat

Envia mensajes de text a cada uno de los miembros en tiempo real
con fecha y hora.

*********************Fuentes de referencia.****************
Para realizar el proyecto tomamos como base el tutorial que se muestra a continuacion
https://www.youtube.com/watch?v=gPqJcPtN18I&list=PLxefhmF0pcPmtdoud8f64EpgapkclCllj