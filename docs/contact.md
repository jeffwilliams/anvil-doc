# Contact

Questions or comments? Reach out at <span id="addr"></span>

<script>

function a() {
  a = document.getElementById("addr")
  if (!a) {
    console.log("No 'addr' element")
    return
  }

  s = String.fromCodePoint(0x40);
  com = "<!--last ditch effort-->"
  s = com + s + com
  s = "o" + s
  s = "f" + s
  s = "n" + s
  s = "i" + s
  s = s + "anvil-editor.net"
  a.innerHTML = s
}
a()

</script>


A community server is available in [Discord](https://discord.gg/JvMjPQhvQy), and you can discuss Anvil on [Reddit](https://www.reddit.com/r/anvil_text_editor/). 
