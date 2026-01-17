const express = require("express");

const app = express();
app.use(express.json());

app.get("/barcode/:code", async (req, res) => {
  const response = await fetch(
    `https://world.openfoodfacts.org/api/v0/product/${req.params.code}.json`
  );
  const data = await response.json();

  if (!data.product) {
    return res.status(404).json({ error: "Not found" });
  }

  const p = data.product.nutriments || {};
  res.json({
    calories: p["energy-kcal_100g"] || 0,
    protein: p["proteins_100g"] || 0,
    carbs: p["carbohydrates_100g"] || 0,
    fat: p["fat_100g"] || 0
  });
});

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log("INTAKE API running"));
