---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: standard keys, import keys, encryption keys, Hyper Protect Crypto Services GUI

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 匯入標準金鑰
{: #import-standard-keys}

您可以使用 {{site.data.keyword.hscrypto}} GUI 或使用 {{site.data.keyword.hscrypto}} API 透過程式設計方式，來新增現有加密金鑰。

## 使用 GUI 匯入標準金鑰
{: #gui}

[在建立服務的實例之後](/docs/services/hs-crypto/provision.html)，請完成下列步驟以使用 {{site.data.keyword.hscrypto}} GUI 來輸入現有標準金鑰。

1. [登入 {{site.data.keyword.cloud_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/){: new_window}。
2. 從 {{site.data.keyword.cloud_notm}} 儀表板，選取已佈建的 {{site.data.keyword.hscrypto}} 實例。
3. 若要匯入新金鑰，請按一下**新增金鑰**，然後選取**輸入現有金鑰**視窗。

    指定金鑰的詳細資料：

    <table>
      <tr>
        <th>設定</th>
        <th>說明</th>
      </tr>
      <tr>
        <td>名稱</td>
        <td>
          <p>方便識別金鑰且人類可閱讀的唯一別名。</p>
          <p>若要保護您的隱私權，請確定金鑰名稱未包含個人識別資訊 (PII)（例如您的姓名或位置）。</p>
        </td>
      </tr>
      <tr>
        <td>金鑰類型</td>
        <td>您要在 {{site.data.keyword.hscrypto}} 中管理的<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">金鑰類型</a>。從金鑰類型清單中，選取<b>標準金鑰</b>。</td>
      </tr>
      <tr>
        <td>金鑰資料</td>
        <td>
          <p>您要在服務中管理並以 base64 編碼的金鑰資料（例如對稱金鑰）。</p>
          <p>請確定金鑰資料滿足下列需求：</p>
          <p><ul>
              <li>金鑰大小最多可以為 10,000 個位元組。</li>
              <li>資料位元組必須以 base64 編碼。</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明<b>產生新金鑰</b>設定</caption>
    </table>

4. 當您填寫完金鑰的詳細資料時，請按一下**產生金鑰**以便確認。

## 使用 API 建立標準金鑰
{: #api}

對下列端點發出 `POST` 呼叫來建立標準金鑰：

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/hs-crypto/access-api.html)。

1. 使用下列 cURL 指令，來呼叫 [{{site.data.keyword.hscrypto}} API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
    "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>",
       "extractable": <key_type>
       }
     ]
    }'
    ```
    {: codeblock}

    若要在您帳戶的 Cloud Foundry 組織及空間內使用金鑰，請將 `Bluemix-Instance` 取代為適當的 `Bluemix-org` 及 `Bluemix-space` 標頭。[如需相關資訊，請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。
    {: tip}

    根據下表取代範例要求中的變數。
    <table>
      <tr>
        <th>變數</th>
        <th>說明</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>代表 {{site.data.keyword.hscrypto}} 服務實例所在地理區域的地區縮寫，例如 <code>us-south</code> 或 <code>eu-gb</code>。如需相關資訊，請參閱<a href="/docs/services/hs-crypto/regions.html#endpoints">地區服務端點</a>。</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>您的 {{site.data.keyword.cloud_notm}} 存取記號。請在 cURL 要求中包含 <code>IAM</code> 記號的完整內容，包括 Bearer 值。如需相關資訊，請參閱<a href="/docs/services/hs-crypto/access-api.html#retrieve-token">擷取存取記號</a>。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>指派給您的 {{site.data.keyword.hscrypto}} 服務實例的唯一 ID。如需相關資訊，請參閱<a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">擷取實例 ID</a>。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>選用項目：變更 <code>POST</code> 及 <code>DELETE</code> 作業之伺服器行為的標頭。</p><p>當您將 <em>return_preference</em> 變數設為 <code>return=minimal</code> 時，服務在回應實體內文中只會傳回金鑰 meta 資料（例如金鑰名稱及 ID 值）。當您將變數設為 <code>return=representation</code> 時，服務會傳回金鑰資料及金鑰 meta 資料。</p></td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>方便識別金鑰且人類可閱讀的唯一名稱。</p>
          <p>重要事項：若要保護您的隱私權，請不要將個人資料儲存為金鑰的 meta 資料。</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>選用項目：金鑰的延伸說明。</p>
          <p>重要事項：若要保護您的隱私權，請不要將個人資料儲存為金鑰的 meta 資料。</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>選用項目：系統中的金鑰到期的日期和時間，以 RFC 3339 格式表示。如果省略 <code>expirationDate</code> 屬性，則金鑰不會到期。</td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>您要在服務中管理並以 base64 編碼的金鑰資料（例如對稱金鑰）。</p>
          <p>請確定金鑰資料滿足下列需求：</p>
          <p><ul>
              <li>金鑰大小最多可以為 10,000 個位元組。</li>
              <li>資料位元組必須以 base64 編碼。</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>決定金鑰資料是否可以離開服務的布林值。</p>
          <p>當您將 <code>extractable</code> 屬性設為 <code>true</code> 時，服務會將金鑰指定為標準金鑰，您可以將它儲存在應用程式或服務中。</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">表 2. 說明使用 {{site.data.keyword.hscrypto}} API 新增標準金鑰所需的變數</caption>
    </table>

    若要保護您個人資料的機密性，請在將金鑰新增至服務時避免輸入個人識別資訊 (PII)（例如您的姓名或位置）。如需其他 PII 範例，請參閱 [NIST 特殊出版品 800-122 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window} 的第 2.2 節。
    {: tip}

    成功的 `POST /v2/keys` 回應會傳回您金鑰的 ID 值，以及其他 meta 資料。ID 是指派給您金鑰的唯一 ID，並用於後續的 {{site.data.keyword.hscrypto}} API 呼叫。

2. 選用項目：執行下列呼叫來取得 {{site.data.keyword.hscrypto}} 服務實例中的金鑰，確認已新增金鑰。

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### 下一步為何？

- 若要進一步瞭解如何以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。
- 若要查看 {{site.data.keyword.hscrypto}} 中所儲存的金鑰如何運作來加密及解密資料的範例，請[試用 GitHub 中的範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}。
