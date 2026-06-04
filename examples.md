# carp-dynamics Examples

## 1. Simple Particle with Gravity
This example shows how to set up a basic particle simulation where an object falls under gravity and experiences air resistance (damping).

```clojure
(load "dynamics.carp")
(use Body)
(use Integrator)
(use Transform)
(use Vector3)

(defn main []
  (let [trans (Transform.identity)
        ;; Mass=1.0, Bounciness=0.5, Friction=0.5, Damping=0.9
        body (Body.new 1.0 0.5 0.5 0.9)]
    (while true
      (let [dt 0.016]
        (do
          ;; Apply Gravity
          (Body.apply-force! &body &(Vector3.init 0.0 -9.81 0.0))
          
          ;; Integrate
          (Integrator.step! &trans &body dt)
          
          (println* "Current Position: " (Vector3.str (Transform.position &trans))))))))
```

## 2. Setting up a Static Floor
Static bodies are immune to forces and integration. They are used for the "immovable" parts of your world.

```clojure
(load "dynamics.carp")
(use Body)
(use Transform)
(use Vector3)

(defn setup-world []
  (let [floor-trans (Transform.init (Vector3.init 0.0 -1.0 0.0) 
                                   (Quaternion.identity) 
                                   (Vector3.init 100.0 1.0 100.0))
        floor-body (Body.static)]
    (do
      (println* "Static floor initialized at Y=-1.0"))))
```

## 3. Immediate Impulses
Unlike continuous forces, impulses change velocity instantly. This is perfect for jumps, explosions, or recoil.

```clojure
(load "dynamics.carp")
(use Body)
(use Vector3)

(defn jump [body]
  ;; Add 5.0 units of upward velocity instantly
  (Body.apply-impulse! body &(Vector3.init 0.0 5.0 0.0)))
```
