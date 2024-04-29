---
title: Week 7 Blog
published_at: 2024-04-30
snippet: Week 7 Homework - Combining ideas / libraries
disable_html_sanitization: true
---

Combination of ideas: [Perlin from c2.js](https://github.com/ren-yuan/c2.js/blob/main/examples/Perlin.js) and [ascii cam](https://blog.science.family/240412_ascii_cam)

<script src="/scripts/c2/c2.min.js"></script>

<canvas id="c2"></canvas>
<div id="ascii_div"></div>

<script>
    //Created by Ren Yuan

    const renderer = new c2.Renderer(document.getElementById('c2'));
    resize();

    renderer.background('#cccccc');
    let perlin = new c2.Perlin();
    //perlin.detail(4, .5);
    //perlin.seed(0);


    let row = 20;
    let col = 10;

    const chars = "perlin"

    const div = document.getElementById (`ascii_div`)
    div.style.fontFamily = `monospace`
    div.style.textAlign = `center`

    renderer.draw(() => {
        renderer.clear();

        let time = renderer.frameCount * .01;

        renderer.stroke('#333333');
        renderer.lineWidth(1);
        for (let i=0; i<row; i++) {
        let t = c2.norm(i, 0, row);
        let c = c2.Color.hsl(30*t, 30+30*t, 20+70*t);
        renderer.fill(c);
        renderer.beginPath();
        for (let j=0; j<col; j++) {
            let x = c2.map(j, 0, col-1, 0, renderer.width);
            let y = c2.map(i, 0, row, renderer.height/3, renderer.height)
            + (perlin.noise(time+j*.1, time+i*.04)-.5)
            * renderer.height*2;
            renderer.lineTo(x, y);
        }
        renderer.lineTo(renderer.width, renderer.height);
        renderer.lineTo(0, renderer.height);
        renderer.endPath(true);
        }

        const w = renderer.canvas.width
        const h = renderer.canvas.height
        const pixels = renderer.context.getImageData (0, 0, w, h).data

        let ascii_img = ``

        for (let y = 0; y < h; y += 22) {
            for (let x = 0; x < w; x += 10) {
                const i = (y * w + x) * 4
                const r = pixels[i]
                const g = pixels[i + 1]
                const b = pixels[i + 2]
                const br = (r * g * b / 16581376) ** 0.1
                const char_i = Math.floor (br * chars.length)
                ascii_img += chars[char_i]
            }
            ascii_img += `\n`
        }

        div.innerText = ascii_img
    });


    window.addEventListener('resize', resize);
    function resize() {
        let parent = renderer.canvas.parentElement;
        renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
    }

</script>

## Process (remove this title later)

- take code from c2 library and combine the ascii code in the 'draw' function
- hide the first c2 canvas