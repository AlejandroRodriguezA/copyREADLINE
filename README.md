# copyREADLINE
Copy to clipboard from terminal
## Motivo.
Estoy usando zsh y kitty y frecuentemente necesito copiar el comando del terminal a otro programa, entonces la mejor forma es configurar el ~/.zshrc.
## Referencia.
Buscando y buscando la mejor opcion que encontre fueron:
  * https://unix.stackexchange.com/questions/51933/zsh-copy-and-paste-like-emacs
  * http://stchaz.free.fr/mouse.zsh

## Requisitos:
Yo utilizo [xclip](https://github.com/astrand/xclip), pero tambien se puede utilizar [xcel](https://github.com/kfish/xsel),

## ~/.zshrc

```
pb-kill-whole-line(){
zle kill-whole-line
print -rn $CUTBUFFER | xclip -selection clipboard
}
zle -N pb-kill-whole-line
bindkey -e '^u' pb-kill-whole-line

pb-kill-line () {
  zle kill-line
  print -rn $CUTBUFFER | xclip -selection clipboard
}
zle -N pb-kill-line
bindkey -e '^k' pb-kill-line
```

## Explicacion:
Antes en el terminal ejecutamos `bindkey` para ver que Ctrl+u (kill-whole-line) y Ctrl+k (kill-line) son las combinaciones que estoy buscando.

1- Definimos dos funciones **pb-kill-whole-line** y **pb-kill-lin**
  - Ejecuta la misma funcion definida por defecto.
  - Guarda el resultado en la variable $CUTBUFFER y la redireciona al clipboard usando xclip
2- Ejecutamos la funcion
3- Redifinimos las **bindkey** para que hagan lo mismo que hacian, pero adicionalmente agregen el contenido al clipboard. **NOTA**: Como estoy usando el ***emacs mode*** la opcion para el bindkey es **-e**.
