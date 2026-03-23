# FormAPI Craft

**Visual Form Builder for PocketMine-MP** — drag-and-drop constructor for FormAPI forms with live Minecraft Bedrock preview and instant PHP code export.

Stop writing button arrays by hand. Design your forms visually, see exactly how they'll look in-game, and export clean PHP code in one click.

![License](https://img.shields.io/badge/license-MIT-green)
![PocketMine](https://img.shields.io/badge/PocketMine--MP-5.x-blue)

---

## Features

- **3 form types** — SimpleForm (buttons), ModalForm (yes/no), CustomForm (inputs, sliders, dropdowns, toggles)
- **Live Minecraft preview** — see your form exactly as it appears in Bedrock Edition
- **Click to add elements** — buttons, inputs, sliders, dropdowns, step sliders, toggles, labels
- **Properties panel** — edit text, icons, options, default values in real time
- **Reorder & duplicate** — move elements up/down, duplicate with one click
- **Button icons** — supports both texture paths (`textures/items/diamond`) and URLs
- **PHP code export** — generates valid, ready-to-use code with proper closures
- **Two libraries supported**:
  - [jojoe77777/FormAPI](https://github.com/jojoe77777/FormAPI) — classic, most popular
  - [dktapps/pmforms](https://github.com/dktapps-pm-pl/pmforms) — modern, type-safe
- **Import/Export JSON** — save and share form configurations
- **Zero dependencies** — single HTML file, works offline, no build step
- **Mobile-friendly** — responsive layout

## Quick Start

1. Open `index.html` in any browser
2. Choose form type (Simple / Modal / Custom)
3. Add elements from the left panel
4. Click elements on the preview to edit properties
5. Hit **Export PHP** and copy the code into your plugin

Or use the hosted version: **[w1zardz.github.io/formapi-craft](https://w1zardz.github.io/formapi-craft/)**

## Supported Elements

| Element | Form Type | Description |
|---------|-----------|-------------|
| Button | SimpleForm | Clickable button with optional icon (path/URL) |
| Input | CustomForm | Text input field with placeholder and default |
| Dropdown | CustomForm | Select from a list of options |
| Slider | CustomForm | Numeric slider (min/max/step) |
| StepSlider | CustomForm | Step-based slider with named steps |
| Toggle | CustomForm | On/off switch |
| Label | CustomForm | Static text label |

## Example Output

### SimpleForm (FormAPI)
```php
use jojoe77777\FormAPI\SimpleForm;

$form = new SimpleForm(function(Player $player, ?int $data): void {
    if ($data === null) return;

    match ($data) {
        0 => $player->sendMessage("Играть"),
        1 => $player->sendMessage("Настройки"),
    };
});

$form->setTitle("Главное меню");
$form->setContent("Выберите действие:");

$form->addButton("Играть", 0, "textures/items/diamond_sword");
$form->addButton("Настройки");

$player->sendForm($form);
```

### CustomForm (pmforms)
```php
use dktapps\pmforms\CustomForm;
use dktapps\pmforms\CustomFormResponse;
use dktapps\pmforms\element\Input;
use dktapps\pmforms\element\Slider;
use dktapps\pmforms\element\Toggle;

$form = new CustomForm(
    "Настройки игрока",
    [
        new Input("Никнейм", "Введите ник..."),
        new Slider("Громкость", 0, 100, 1, 50),
        new Toggle("PvP", true),
    ],
    onSubmit: function(Player $player, CustomFormResponse $response): void {
        $nickname = $response->getString(0);
        $volume = $response->getFloat(1);
        $pvp = $response->getBool(2);
    },
    onClose: function(Player $player): void {
        // Closed
    }
);

$player->sendForm($form);
```

## How It Works

FormAPI Craft is a single-page web application. All processing happens in the browser — no server, no tracking, no data collection. Your forms never leave your machine.

The Minecraft preview uses CSS styling that closely mimics the Bedrock Edition form UI, so what you see is what players will see in-game.

## Contributing

PRs and issues are welcome! If you have ideas for new features:

- New element types
- Better Minecraft preview accuracy
- Code generation for other form libraries
- Localization

## Related Tools

- [Bedrock Glyph Drawer](https://github.com/w1zardz/bedrock-glyph-drawer) — Pixel editor for Minecraft Bedrock custom fonts and glyphs

## Built With

- Vanilla HTML/CSS/JS — no frameworks, no build tools
- Minecraft Bedrock UI reference for preview styling

## PocketBot

This project is submitted to **PocketBot** — the PocketMine-MP community bot for discovering tools and plugins.

## License

MIT License — use it however you want.

---

Made with care for the PocketMine-MP community.
