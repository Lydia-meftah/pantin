# Build — Vertical slice, étape 1 (le Pantin bouge)

But : un Pantin contrôlable qui marche, saute et titube dans une salle sombre.
Dessiné en primitives (pas de sprite à créer). 3 objets, 1 room.

## 1. obj_mur  (le sol et les plateformes)

- Objet solide, invisible (décoche « Visible » ou laisse vide).
- Aucun code. Sert juste de collision.

## 2. obj_pantin  (le perso)

### Événement Create
```gml
move_speed = 2.2;   // lent, maladroit
grav       = 0.4;
jump_force = -8;
hsp = 0;
vsp = 0;
wobble = 0;         // le ballant / la maladresse
facing = 1;
```

### Événement Step
```gml
var move = keyboard_check(vk_right) - keyboard_check(vk_left);
hsp = move * move_speed;
if (move != 0) facing = sign(move);

vsp += grav;

var on_ground = place_meeting(x, y + 1, obj_mur);
if (on_ground && keyboard_check_pressed(vk_space)) vsp = jump_force;

if (place_meeting(x + hsp, y, obj_mur)) {
    while (!place_meeting(x + sign(hsp), y, obj_mur)) x += sign(hsp);
    hsp = 0;
}
x += hsp;

if (place_meeting(x, y + vsp, obj_mur)) {
    while (!place_meeting(x, y + sign(vsp), obj_mur)) y += sign(vsp);
    vsp = 0;
}
y += vsp;

if (abs(hsp) > 0) wobble += 0.25; else wobble *= 0.85;
```

### Événement Draw
```gml
var sway = sin(wobble) * 3;

draw_set_alpha(0.35);
draw_set_colour(c_black);
draw_ellipse(x - 18, y - 4, x + 18, y + 4, false);
draw_set_alpha(1);

draw_set_colour(make_colour_rgb(216, 202, 180));   // corps chiffon
draw_ellipse(x - 16 + sway, y - 34, x + 16 + sway, y - 4, false);
draw_ellipse(x - 14 + sway, y - 62, x + 14 + sway, y - 34, false);   // tête

draw_set_colour(make_colour_rgb(149, 167, 190));   // bonnet
draw_triangle(x - 10 + sway, y - 58, x + 2 + sway, y - 82, x + 10 + sway, y - 56, false);

draw_set_colour(make_colour_rgb(43, 38, 34));      // yeux endormis
draw_line_width(x - 7 + sway, y - 50, x - 2 + sway, y - 50, 2);
draw_line_width(x + 2 + sway, y - 50, x + 7 + sway, y - 50, 2);

draw_set_colour(c_white);
draw_set_alpha(1);
```

## 3. Room  rm_s1_eveil

- Fond très sombre (bleu-nuit, ex. RGB 16,20,29).
- Place une bande de `obj_mur` en bas = le sol.
- Ajoute 2-3 `obj_mur` surélevés = des plateformes.
- Place **un** `obj_pantin` au-dessus du sol.
- Lance (F5 / `gm-cli run`). Flèches = marcher, Espace = sauter.

## Ensuite (étape 2)
Une porte `obj_porte` au bout de la salle qui, touchée, passe à la room
suivante — puis on branchera la première énigme (cryptogramme mural).
