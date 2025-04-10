# wwii-ballistics
Excellent — you're diving into real **WWII-grade ballistics**, and that's both historically rich and physically deep. If you wanted to **calculate this by hand**, including **air drag, gravity, and other real factors**, it would require some approximation methods and manual iterations. Let's break down how you'd do this without a computer, as they did with **analog fire control systems** in the 1940s.

---

## 🧠 1. **Manual Calculation Approach: Overview**

You'd simulate the projectile’s motion in **small time steps** (e.g. every 0.1 or 0.2 seconds), recalculating the projectile's **velocity, position, and acceleration** at each step.

The process follows **Newton's laws**, split into horizontal and vertical components.

---

## 🧾 2. **Data You'd Need (Example for 16-inch shell)**

| Parameter                     | Value                    |
|------------------------------|--------------------------|
| Mass                         | 1225 kg                  |
| Initial speed (v₀)           | 760 m/s                  |
| Launch angle (θ)             | 14°                      |
| Gravity (g)                  | 9.81 m/s²                |
| Air density (ρ)              | 1.225 kg/m³              |
| Drag coefficient (Cd)        | 0.3                      |
| Cross-sectional area (A)     | ≈ 0.129 m²               |
| Time step (Δt)               | 0.1 s                    |

---

## 🧮 3. **Manual Iterative Method (Step-by-Step)**

### 👉 Step 1: Initialize
Convert angle θ to radians, and calculate initial `vx` and `vy`:

\[
\theta = 14^\circ = 0.244 \text{ rad}
\]
\[
v_{x0} = v_0 \cdot \cos(\theta) \approx 738.2 \text{ m/s}
\]
\[
v_{y0} = v_0 \cdot \sin(\theta) \approx 183.8 \text{ m/s}
\]

### 👉 Step 2: For each time step

At each step `n`:
1. **Calculate speed:**  
\[
v = \sqrt{v_x^2 + v_y^2}
\]

2. **Compute drag force:**  
\[
F_d = \frac{1}{2} \cdot \rho \cdot C_d \cdot A \cdot v^2
\]

3. **Resolve drag into components:**
\[
a_{dx} = \frac{F_d \cdot \frac{v_x}{v}}{m}
\quad\text{and}\quad
a_{dy} = \frac{F_d \cdot \frac{v_y}{v}}{m}
\]

4. **Update acceleration:**
\[
a_x = -a_{dx}
\quad\text{and}\quad
a_y = -g - a_{dy}
\]

5. **Update velocity:**
\[
v_x^{(n+1)} = v_x^{(n)} + a_x \cdot \Delta t
\quad\text{and}\quad
v_y^{(n+1)} = v_y^{(n)} + a_y \cdot \Delta t
\]

6. **Update position:**
\[
x^{(n+1)} = x^{(n)} + v_x \cdot \Delta t
\quad\text{and}\quad
y^{(n+1)} = y^{(n)} + v_y \cdot \Delta t
\]

7. **Repeat** until \( y < 0 \)

---

## 📚 4. How They Did It in WWII

WWII fire control teams used:
- **Range tables** calculated in advance
- **Mechanical analog computers** (e.g., Mk I Fire Control Computer)
- **Manual adjustments** for:
  - Wind speed/direction
  - Temperature
  - Humidity
  - Altitude
  - Barrel wear

They would interpolate between **known precomputed values**, much like you’d use a slide rule.

---

## 🌍 5. To Add More Realism:

Here’s how you’d simulate **all the real factors**, manually:

| Factor              | Manual Approach                                                                 |
|---------------------|----------------------------------------------------------------------------------|
| **Air drag**        | Use iterative drag formulas per time step (as above)                            |
| **Wind**            | Adjust `vx` by wind component, and add to drag calculation                      |
| **Air density**     | Varies with altitude → use ISA model: ρ(y) = ρ₀ × exp(-y/H)                      |
| **Coriolis effect** | Include a lateral acceleration term based on latitude and velocity              |
| **Humidity/temp**   | Modify air density accordingly (affects drag force)                             |
| **Target motion**   | Calculate target's predicted future location at impact time                     |

---

## ✍️ Would You Like a Worksheet?

I can generate a PDF-style **manual worksheet** where you can follow and fill each column:
- Time
- Position
- Velocity
- Drag
- Acceleration

Or I can break it into a **notebook-friendly format** for practice.

Would you like that? Or would you prefer we step through a full example together by hand here, one iteration at a time?
