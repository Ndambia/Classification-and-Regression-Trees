# Reading the data
df = pd.read_csv("datasets/diabetes.csv")

# FEATURE ENGINEERING
##################################################



df.loc[(df["Age"] <= 18 ), "NEW_AGE"] = "young"
df.loc[(df["Age"] > 18 ) & (df["Age"] <= 24), "NEW_AGE"] = "adult"
df.loc[(df["Age"] > 24 ) & (df["Age"] <= 59), "NEW_AGE"] = "mid_adult"
df.loc[(df["Age"] > 59), "NEW_AGE"] = "senior"



df.loc[(df["BMI"] < 18.5) , "BMI_CAT"] ="underweight"
df.loc[(df["BMI"] >= 18.5) & (df["BMI"] < 24.9) , "BMI_CAT"] ="normal"
df.loc[(df["BMI"] >= 24.9) & (df["BMI"] < 29.9) , "BMI_CAT"]="overweight"
df.loc[(df["BMI"] >= 29.9) , "BMI_CAT"] ="obese"



df.loc[(df["Insulin"] < 15) , "INSULIN_CAT"] ="low"
df.loc[(df["Insulin"] >= 15) & (df["Insulin"] < 166) , "INSULIN_CAT"] ="normal"
df.loc[(df["Insulin"] >= 166) , "INSULIN_CAT"] ="high"

  
# One Hot Encoding
ohe_cols = [col for col in df.columns if 10 >= df[col].nunique() > 2]
df= pd.get_dummies(df,columns= ohe_cols, drop_first=True)          


X = df.drop(["Outcome"], axis=1)
y = df["Outcome"]

