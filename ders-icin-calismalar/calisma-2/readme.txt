Yemek tarifleri domainini, bu alanın çok sayıda varlık (malzeme, tarif, tat, teknik vs.) ve bu varlıklar arasında zengin ilişki türleri içermesinden dolayı seçtim.
•	Aynı malzemeyi kullanan farklı tarifleri kolayca bulmak,
•	Belirli bir tat profiline sahip tarifleri listelemek,
•	Elindeki malzemeye göre tarif önerme,
•	Bir malzemenin yerine kullanılabilecek alternatifleri göstermek gibi işlemler yapabilirim. 
Ayrıca, bu konu günlük yaşamla bağlantılı ve anlaşılması kolay olduğu için modellemeyi de daha anlaşılır hale getiriyor.

// -------- MALZEMELER --------
MERGE (Sugar:Ingredient {name: "Şeker"}) ON CREATE SET Sugar.category = "Tatlandırıcı";
MERGE (Milk:Ingredient {name: "Süt"}) ON CREATE SET Milk.category = "Süt Ürünü";
MERGE (Egg:Ingredient {name: "Yumurta"}) ON CREATE SET Egg.category = "Hayvansal";
MERGE (Flour:Ingredient {name: "Un"}) ON CREATE SET Flour.category = "Tahıl";
MERGE (Butter:Ingredient {name: "Tereyağı"}) ON CREATE SET Butter.category = "Süt Ürünü";
MERGE (Vanilla:Ingredient {name: "Vanilin"}) ON CREATE SET Vanilla.category = "Aroma";
MERGE (Cream:Ingredient {name: "Krema"}) ON CREATE SET Cream.category = "Süt Ürünü";
MERGE (Chocolate:Ingredient {name: "Çikolata"}) ON CREATE SET Chocolate.category = "Tatlandırıcı";
MERGE (Gelatin:Ingredient {name: "Jelatin"}) ON CREATE SET Gelatin.category = "Katılaştırıcı";
MERGE (Honey:Ingredient {name: "Bal"}) ON CREATE SET Honey.category = "Doğal Tatlandırıcı";
MERGE (Biscuit:Ingredient {name: "Bisküvi"}) ON CREATE SET Biscuit.category = "Hazır Gıda";
MERGE (Cinnamon:Ingredient {name: "Tarçın"}) ON CREATE SET Cinnamon.category = "Baharat";
MERGE (Rice:Ingredient {name: "Pirinç"}) ON CREATE SET Rice.category = "Tahıl";

// -------- LEZZETLER --------
MERGE (Sweet:Flavor {name: "Tatlı"});
MERGE (Creamy:Flavor {name: "Kremamsı"});
MERGE (Caramel:Flavor {name: "Karamelli"});

// -------- TEKNİKLER --------
MERGE (Bake:Technique {name: "Fırınlama"});
MERGE (Boil:Technique {name: "Kaynatma"});
MERGE (Mix:Technique {name: "Karıştırma"});
MERGE (Chill:Technique {name: "Soğutma"});

// -------- TARİFLER --------
MERGE (Pudding:Recipe {name: "Sütlaç"})
  ON CREATE SET Pudding.difficulty = "Kolay", Pudding.time_minutes = 45;
MERGE (Cake:Recipe {name: "Kek"})
  ON CREATE SET Cake.difficulty = "Orta", Cake.time_minutes = 60;
MERGE (Cheesecake:Recipe {name: "Cheesecake"})
  ON CREATE SET Cheesecake.difficulty = "Zor", Cheesecake.time_minutes = 90;
MERGE (Truffle:Recipe {name: "Çikolata Truffle"})
  ON CREATE SET Truffle.difficulty = "Kolay", Truffle.time_minutes = 30;
MERGE (Magnolia:Recipe {name: "Magnolia"})
  ON CREATE SET Magnolia.difficulty = "Orta", Magnolia.time_minutes = 50;

// -------- MALZEME-İÇERİK İLİŞKİLERİ --------
MATCH (r:Recipe {name: "Sütlaç"}), (i:Ingredient {name: "Şeker"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Sütlaç"}), (i:Ingredient {name: "Süt"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Sütlaç"}), (i:Ingredient {name: "Vanilin"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Sütlaç"}), (i:Ingredient {name: "Pirinç"}) MERGE (r)-[:CONTAINS]->(i);

MATCH (r:Recipe {name: "Kek"}), (i:Ingredient {name: "Un"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Kek"}), (i:Ingredient {name: "Yumurta"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Kek"}), (i:Ingredient {name: "Şeker"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Kek"}), (i:Ingredient {name: "Tereyağı"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Kek"}), (i:Ingredient {name: "Vanilin"}) MERGE (r)-[:CONTAINS]->(i);

MATCH (r:Recipe {name: "Cheesecake"}), (i:Ingredient {name: "Krema"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Cheesecake"}), (i:Ingredient {name: "Bisküvi"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Cheesecake"}), (i:Ingredient {name: "Tereyağı"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Cheesecake"}), (i:Ingredient {name: "Şeker"}) MERGE (r)-[:CONTAINS]->(i);

MATCH (r:Recipe {name: "Çikolata Truffle"}), (i:Ingredient {name: "Çikolata"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Çikolata Truffle"}), (i:Ingredient {name: "Krema"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Çikolata Truffle"}), (i:Ingredient {name: "Tereyağı"}) MERGE (r)-[:CONTAINS]->(i);

MATCH (r:Recipe {name: "Magnolia"}), (i:Ingredient {name: "Süt"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Magnolia"}), (i:Ingredient {name: "Un"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Magnolia"}), (i:Ingredient {name: "Şeker"}) MERGE (r)-[:CONTAINS]->(i);
MATCH (r:Recipe {name: "Magnolia"}), (i:Ingredient {name: "Tarçın"}) MERGE (r)-[:CONTAINS]->(i);

// -------- LEZZET İLİŞKİLERİ --------
MATCH (r:Recipe {name: "Sütlaç"}), (f:Flavor {name: "Tatlı"}) MERGE (r)-[:HAS_FLAVOR]->(f);
MATCH (r:Recipe {name: "Cheesecake"}), (f:Flavor {name: "Kremamsı"}) MERGE (r)-[:HAS_FLAVOR]->(f);
MATCH (r:Recipe {name: "Çikolata Truffle"}), (f:Flavor {name: "Karamelli"}) MERGE (r)-[:HAS_FLAVOR]->(f);
MATCH (r:Recipe {name: "Kek"}), (f:Flavor {name: "Tatlı"}) MERGE (r)-[:HAS_FLAVOR]->(f);
MATCH (r:Recipe {name: "Magnolia"}), (f:Flavor {name: "Kremamsı"}) MERGE (r)-[:HAS_FLAVOR]->(f);

// -------- TEKNİK İLİŞKİLERİ --------
MATCH (r:Recipe {name: "Sütlaç"}), (t:Technique {name: "Kaynatma"}) MERGE (r)-[:USES_TECHNIQUE]->(t);
MATCH (r:Recipe {name: "Kek"}), (t:Technique {name: "Fırınlama"}) MERGE (r)-[:USES_TECHNIQUE]->(t);
MATCH (r:Recipe {name: "Cheesecake"}), (t:Technique {name: "Fırınlama"}) MERGE (r)-[:USES_TECHNIQUE]->(t);
MATCH (r:Recipe {name: "Çikolata Truffle"}), (t:Technique {name: "Karıştırma"}) MERGE (r)-[:USES_TECHNIQUE]->(t);
MATCH (r:Recipe {name: "Magnolia"}), (t:Technique {name: "Soğutma"}) MERGE (r)-[:USES_TECHNIQUE]->(t);

// -------- YERİNE KULLANILABİLİR MALZEME İLİŞKİLERİ --------
MATCH (i1:Ingredient {name: "Bal"}), (i2:Ingredient {name: "Şeker"}) MERGE (i1)-[:CAN_REPLACE]->(i2);
MATCH (i1:Ingredient {name: "Şeker"}), (i2:Ingredient {name: "Bal"}) MERGE (i1)-[:CAN_REPLACE]->(i2);
