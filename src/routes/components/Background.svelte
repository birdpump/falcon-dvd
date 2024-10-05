<script>
    import { Layer } from 'svelte-canvas';

    const setup = ({ context, width, height }) => {
        // Set the background color
        context.fillStyle = "#222"; // Solid color for the background
        context.fillRect(0, 0, width, height); // Fill the entire canvas with the solid color
    }

    const render = ({ context, width, height }) => {
        // Clear the canvas before rendering the background and the image
        context.clearRect(0, 0, width, height);

        // Set the background color again (you can also set it in setup)
        context.fillStyle = "#222"; // Solid background color
        context.fillRect(0, 0, width, height); // Fill the canvas

        // Draw any additional content here if needed
    }
</script>

<Layer {setup} {render} />
