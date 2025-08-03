```mermaid

%%{ init : {
    "theme": "base",
    "themeVariables": {
      "primaryColor": "#b8c37eff",
      "primaryTextColor": "#052031ff",
      "primaryBorderColor": "#525e1bff",
      "lineColor": "#aab3bbff",
      "tertiaryColor": "#F9E79F",
      "fontSize": "14px"
    }
  } }%%

flowchart TD

    %% === Nodes ===
    A[Start<br>Library and data import]:::inicio
    B[EDA:<br>Account_Number distribution<br>Contingency between Supplier_Code and Account_Number<br>Cramér's V = 0.842<br>p-value = 0.000]:::bloco
    C[Conclusion:<br>Strong association between supplier and accounting account]:::resultado

    D[Create Input_Text:<br>Item_Description + 'SUPPLIER_' + Supplier_Name]:::etapa
    E[Create Log_Item_Value using log1p]:::etapa

    F[Split into df_inv_train and df_inv_test]:::etapa

    G1[Vectorizer experiments:<br>- CountVectorizer<br>- TF-IDF<br>- HashingVectorizer<br><br>Result: Count with highest f1_macro]:::bloco
    G2[Pipeline 1:<br>Input_Text → CountVectorizer → LogisticRegression<br><br>Accuracy = 92%<br>Macro F1 = 0.83]:::resultado

    H1[Add Log_Item_Value and StandardScaler]:::etapa
    H2[Pipeline 2:<br>Input_Text + Item_Value + Log_Item_Value<br><br>Accuracy = 94%<br>Macro F1 = 0.91]:::resultado

    I1[New feature engineering:<br>- Log_Taxes_Credit_Amount<br>- Value_Category 'binned Item_Value'<br>- Standardization of numerical features]:::etapa
    I2[Pipeline 3:<br>Input_Text + Log_Item_Value + Item_Quantity + Taxes_Credit_%<br>+ Log_Taxes_Credit_Amount + Value_Category<br><br>Preprocessing: ColumnTransformer<br>Classifier: LogisticRegression 'balanced']:::etapa
    I3[GridSearchCV:<br>- text max_features: 2000, 3000, 5000<br>- reg. strength C: 0.01, 0.1, 1, 10<br><br>Best model: 3000 features, C=1<br>Macro F1 ≈ 0.97 'train']:::resultado
    I4[Final prediction:<br>Accuracy = 98% '50/51'<br>Only 1 misclassification<br>Goal reached]:::resultado

    Z[End of flow]:::fim

    %% === Connections ===
    A --> B --> C --> D --> E --> F --> G1 --> G2 --> H1 --> H2 --> I1 --> I2 --> I3 --> I4 --> Z

