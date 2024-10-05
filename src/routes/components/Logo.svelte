<script>
    import { Layer } from 'svelte-canvas';
    import { onMount } from 'svelte';

    let logo;
    const w = 603 / 3, h = 494 / 3; // Set image dimensions

    let x = 0,
        y = 0,
        xflip = 1,
        yflip = 1,
        imageLoaded = false;

    // Use onMount to ensure code runs only in the browser
    onMount(() => {
        logo = new Image();
        logo.src = "/flacon1.png"; // Load the image
        logo.onload = () => {
            imageLoaded = true; // Set imageLoaded to true when the image is fully loaded

            // Generate random starting position for x and y
            x = Math.random() * (1152 - w);
            y = Math.random() * (640 - h);
        };
    });

    $: render = ({ context, width, height }) => {
        // Ensure the image has been loaded before attempting to draw it
        if (!imageLoaded) return;

        // Clear the canvas
        context.clearRect(0, 0, width, height);

        // Set the background color
        context.fillStyle = "black"; // Solid background color
        context.fillRect(0, 0, width, height); // Fill the entire canvas with the background color

        // Move the image position
        x += 3.2 * xflip;
        y += 3.2 * yflip;

        // Flip the direction when hitting the edge of the canvas
        if (x <= 0 || x + w >= width) xflip *= -1;
        if (y <= 0 || y + h >= height) yflip *= -1;

        // Draw the image in its original colors
        context.drawImage(logo, x, y, w, h);
    };
</script>

<Layer {render}/>
