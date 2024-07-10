# Dynamic Placeholder Image Generator

A PHP-based tool for generating customized text images on-the-fly. Create dynamic social media graphics, placeholders, or text visuals with custom text, font size, colors, and dimensions via URL parameters.

## Features

- Dynamic text placement with automatic centering
- Customizable background and font colors
- Adjustable image and font sizes
- Automatic text slugification and capitalization
- SEO-friendly URLs with Apache mod_rewrite

## Requirements

- PHP 7.0 or higher
- GD Library
- Apache web server with mod_rewrite enabled
- A TrueType font file (Arial Bold used in this example)

## Installation

1. Clone this repository to your web server:
   ```
   git clone https://github.com/hlotiim/Dynamic-Placeholder-Image-Generator.git
   ```
2. Ensure your web server is configured to run PHP scripts.
3. Update the font file path in the `image_generator.php` script:
   ```php
   $fontFile = __DIR__ . '/path/to/your/Arial_Bold.ttf';
   ```
4. Create or update your `.htaccess` file in the root directory of your website with the following rewrite rule:
   ```apache
   RewriteEngine On
   RewriteRule ^images/([^/]*)/([^/]*)/([^/]*)/([^/]*)/([^/]*)\.png$ image_generator.php?size=$1&bg=$2&fontcolor=$3&sizeandname=$4&text=$5 [L]
   ```

## Usage

Access the script with the following URL format:

```
/images/{size}/{bg}/{fontcolor}/{sizeandname}/{text}.png
```

### Parameters

1. `size`: Font size (integer)
   - Example: `120`
   - This determines the base font size before scaling

2. `bg`: Background color (6-digit hex code without #)
   - Example: `f67280` for a light pink background
   - You can use any valid hex color code

3. `fontcolor`: Text color (6-digit hex code without #)
   - Example: `ffffff` for white text
   - You can use any valid hex color code

4. `sizeandname`: Image dimensions in format WidthxHeight
   - Example: `1200x900`
   - This sets the overall image size in pixels

5. `text`: The text to display on the image
   - Use hyphens instead of spaces
   - The script will automatically capitalize words and wrap long text

### Example URL

```
https://yourdomain.com/images/120/f67280/ffffff/1200x900/hello-world.png
```

This will generate a 1200x900 image with a pink background (#f67280), white text (#ffffff), a base font size of 120, and the text "Hello World" centered on the image.

## Customization

### Editing the Script

You can customize the `image_generator.php` script to modify various aspects of the image generation:

1. **Font**: Change the `$fontFile` variable to use a different TrueType font.
2. **Text Wrapping**: Modify the `wordwrap()` function call to change how long text is wrapped.
3. **Scaling**: Adjust the `$scalingFactor` calculation to change how the font size scales with image size.

### Adding New Features

You can extend the script to add new features, such as:

- Additional text styles (bold, italic, etc.)
- Multiple text lines
- Image overlays or watermarks
- Different text alignments (left, right, etc.)

## Troubleshooting

- If you see a 404 error, ensure your Apache mod_rewrite is enabled and your .htaccess file is correctly placed and readable.
- If the image doesn't generate, check your PHP error logs and ensure the GD library is installed and enabled.
- If the font doesn't render correctly, verify the path to your font file is correct and the file is readable by the web server.

## Security Considerations

- This script doesn't include input sanitization. In a production environment, you should validate and sanitize all input parameters.
- Consider adding rate limiting to prevent abuse of the image generation service.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source and available under the [MIT License](LICENSE).