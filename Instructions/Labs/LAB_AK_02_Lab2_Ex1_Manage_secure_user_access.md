# ラーニング パス 2 - ラボ 2 - 演習 1 - セキュリティで保護されたユーザー アクセスを管理する 

組織は、Microsoft 365 上の会社データへのアクセスが常にセキュリティで保護されていることを保証する必要があります。 Microsoft 365 (ひいては Copilot for Microsoft 365) では、多くの場合、メール、ドキュメント、顧客情報、知的財産など、機密性の高い内密のデータが表示されます。 Microsoft 365 への未承認のアクセスは、データ侵害、なりすまし、その他の悪意のあるアクティビティにつながるおそれがあります。 ユーザー アクセスをセキュリティで保護することで、組織は Microsoft 365 および Copilot for Microsoft 365 内で作業する際に、未承認の個人が会社データにアクセスし、悪用または漏洩する可能性を排除することができます。

次のラボ演習で、あなたは Adatum 社の新しい Microsoft 365 管理者である Holly Dickson として引き続き役割を果たします。 いくつかのユーザー管理機能を実行して、今後の Copilot for Microsoft 365 の展開に向けて Adatum 社の準備を進めます。 まず、Microsoft 365 グローバル管理者ロールを割り当てる、Holly の Microsoft 365 ユーザー アカウントを作成します。 

**注:**  ラボ ホスティング プロバイダーから提供された VM 環境には、20 個を超える既存 Microsoft 365 ユーザー アカウントと、多数の既存オンプレミス ユーザー アカウントが含まれています。 既存 Microsoft 365 ユーザー アカウントのいくつかを、このコースの中のラボ全体で使用します。 MOD 管理者アカウントはラボ ホスティング プロバイダーによって作成されましたが、複数のユーザーに Microsoft 365 グローバル管理者ロールを割り当てることがベスト プラクティスとされているため、Holly Dickson のユーザー アカウントを作成します。 あなたがまだこのプロセスに慣れていない場合には、Microsoft 365 ユーザー アカウントを作成する経験にもなります。

その後、Holly は Adatum 社の CTO から、Microsoft Entra 多要素認証 (MFA)、Microsoft Entra スマート ロックアウトの展開を要請されました。 これらの機能は、Copilot for Microsoft 365 に備えて組織全体のパスワード管理を強化するのに役立ちます。 スマート ロックアウトについては、グループ ポリシー管理を使用して展開します。 

**重要な MFA 通知:** このコースで使用されている Microsoft 365 試用版テナントに対する Microsoft による最近の変更により、このラボに対応する変更を行う必要がありました。 <br/>

**元のラボ設計:** このラボ演習は、もともと Holly Dickson として、タスク 3 で Adatum 社で MFA を有効にする条件付きアクセス ポリシーを作成するように設計されました。 これは、このトレーニングの講義部分で学習したように、MFA を有効にするための推奨される方法です。 タスク 3 では、前の演習で作成した Microsoft 365 パイロット プロジェクト グループのメンバーであるユーザーを除き、すべてのユーザーに対して MFA を有効にする条件付きアクセス ポリシーを作成しました。 タスク 4 でポリシーをテストするために、Adele Vance としてログインしました。 Adele はパイロット プロジェクト グループのメンバーではないため、Microsoft 365 にサインインするには MFA プロセスを完了する必要がありました。 その後、Adele としてサインアウトし、Holly Dickson としてサインインしました。 Holly は Microsoft 365 パイロット プロジェクト グループのメンバーであるため、ユーザー名とパスワードを入力するだけで済みます。 MFA を使用して 2 番目の形式の認証を実行する必要はありませんでした。 タスク 4 のこれら 2 つの手順によって、条件付きアクセス ポリシー が検証されました。 つまり、パイロット プロジェクト グループに含まれていないユーザーのみが MFA を使用する必要がありました。 

このポリシーのもう 1 つの影響は、ラボの残りの部分にサインインするときに、Microsoft 365 パイロット プロジェクト グループのメンバーであった他のテスト ユーザーとして MFA を使用する必要がなかったということです。 MFA からの除外は、会社のビジネス ニーズに応じて実用的な理由で設定できますが、企業は関連するリスクを慎重に評価し、除外を慎重に適用し、常にセキュリティのベスト プラクティスに合わせることを目指す必要があります。 このラボでは、2 つの理由からパイロット プロジェクト グループの除外を作成しました。これにより、条件付きアクセス ポリシーに除外を組み込む方法を学習できます。また、各テスト ユーザーとしてサインインするときにトレーニング ラボで時間を節約する手段としても使用できます。 <br/>

**Microsoft テナントの変更:** つまり、Microsoft はそれ以降、このラボで使用される Microsoft 365 試用版テナントに条件付きアクセス ポリシーを作成し、すべてのユーザー アカウントに対して MFA を要求します。 残念ながら、Microsoft の条件付きアクセス ポリシーは、特定のグループを除外するこのラボで作成する条件付きアクセス ポリシーよりも優先されます。 Microsoft Entra の条件付きアクセス ポリシーは一緒に評価され、ユーザーに適用される最も優先度の高いポリシーが適用されます。 同じ優先度のポリシーが複数存在する場合 (この場合)、最も制限の厳しいポリシーが適用されます。 この場合、Microsoft のポリシーは、ユーザーの例外が含まれるため、作成するポリシーよりも制限が厳しくなっています。 <br/>

**このラボの演習への影響:** Microsoft では条件付きアクセス ポリシーを使用してこの試用版テナントに MFA を適用しますが、タスク 3 で最初に設計された独自の条件付きアクセス ポリシーを作成します。 このタスクは、Microsoft が試用版テナントに組み込んだポリシーを確認できるように、元のバージョンから若干変更されています。 ただし、それ以外に、作成するポリシーは元の設計から変更されていません。Microsoft 365 パイロット プロジェクト グループのメンバーを除き、すべてのユーザーに MFA が必要です。 ただし、Microsoft がラボの試用版テナントに組み込んだポリシーは 2 つのポリシーのより制限が厳しいため、適用時にそのポリシーが優先されます。 このシナリオには 2 つの影響があります。 まず、Microsoft のポリシーでは、これらのラボの残りの部分を通じて各テスト ユーザーとしてサインインするときに MFA を使用する必要があります。 2 つ目は、Microsoft Entra がポリシーを無視するため、テストしても意味がありません。 そのため、作成した条件付きアクセス ポリシーをテストした元のタスク 4 が削除されました。 ポリシーをテストできない場合でも、実際のデプロイでそのエクスペリエンスを得ることができるように、タスク 3 でポリシーを作成する必要があります。 

### タスク 1 - Adatum 社の Microsoft 365 管理者用にユーザー アカウントを作成する

Holly Dickson は、Adatum 社の新しい Microsoft 365 管理者です。 彼女には Microsoft 365 ユーザー アカウントが設定されていないため、前のラボでは最初に MOD 管理者アカウント (既定のグローバル管理者) として Microsoft 365 にサインインしました。 このタスクでは引き続き MOD 管理者としてログインし、その間に Holly 用の Microsoft 365 ユーザー アカウントを作成します。 Microsoft 365 グローバル管理者ロールも Holly のアカウントに割り当てます。 このロールは、Microsoft 365 内ですべての管理機能を実行するのに必要なアクセス許可を Holly に提供します。 このタスクの後は、Holly の新しいアカウントを使用してログインし、残りすべてのラボは Holly のペルソナを使用して実行します。 

**ライセンス ノート:** Holly のアカウントを作成する前に、まず使用可能なライセンスの数をご確認ください。 そうすると、このラボ テナントには 20 個の Microsoft 365 E5 ライセンスと、20 個の Enterprise Mobility + Security E5 ライセンスが用意されていますが、それらのライセンスはすべて、ラボ ホスティング プロバイダーが作成した既存ユーザー アカウントに割り当て済みであることがわかります。 そのため、Holly に割り当てることができるように、まず既存の 1 ユーザーから各ライセンスの割り当てを 1 つ解除する必要があります。

**重要:** 実際に展開する場合のベスト プラクティスとして、常に最初のグローバル管理者アカウントの資格情報を書き留める必要があります (このラボでは、それは MOD 管理者アカウントです。そのユーザー名は admin@xxxxxZZZZZZ.onmicrosoft.com で、xxxxxZZZZZZ の部分はラボ ホスティング プロバイダーから割り当てられたテナント プレフィックスです)。 セキュリティ上の理由から、このアカウント情報を保管する必要があります。 **このアカウントは、個人用設定がない ID である必要があり**、テナント内で可能な最高の特権を有します。 これは個人用設定がないため、MFA をアクティブに**しないでください**。 通常、この最初のグローバル管理者アカウントのユーザー名とパスワードは複数のユーザー間で共有されるため、このアカウントは攻撃するのにうってつけの対象となります。したがって、組織では常に個人用設定のあるサービス管理者アカウント (Exchange 管理者、SharePoint 管理者など) を作成し、かつ可能な限り個人用グローバル管理者を少なく保つことをお勧めします。 実際の展開において作成する個人用グローバル管理者の場合、それぞれを 1 人のユーザー (Holly Dickson など) にマップし、それぞれに Microsoft Entra 多要素認証 (MFA) を適用する必要があります。 つまり、Microsoft は、Microsoft 365 試用版テナントのすべてのユーザーに対して、既定で MFA を既に有効にしています。

1. **LON-CL1** VM 上では、前のラボ演習で **Microsoft 365 管理センター**が Microsoft Edge ブラウザー内で開いたままになっているはずです。 **MOD 管理者**として Microsoft 365 にサインインする必要があります。 

2. 新しいユーザーを追加するので、ユーザー アカウントを追加する前に、まずライセンスを使用することができるかを確認する必要があります。 **[Microsoft 365 管理センター]** のナビゲーション ウィンドウ内で、**[課金情報]** を選択して課金情報のグループを展開し、**[ライセンス]** を選択します。 

3. **[ライセンス]** ページ上では **[サブスクリプション]** タブが既定で表示されます。 サブスクリプションの一覧内で、**[Microsoft 365 E5]** サブスクリプションには使用可能なライセンスがないことに注目してください。 ラボ テナントにはサブスクリプションに 20 個のライセンスが用意されていますが、すべてのライセンスが割り当てられています。 **Microsoft 365 E5** ライセンスを Holly に割り当てる必要があるため、まず既存ユーザー アカウントのライセンス割り当てを解除して、Holly がそれを使用できるようにする必要があります。 

4. **[Microsoft 365 管理センター]** の左側ナビゲーション ウィンドウ内で、**[ユーザー]** を選択してから **[アクティブなユーザー]** を選択します。 **[アクティブなユーザー]** 一覧内には、ラボ ホスティング プロバイダーが作成した既存ユーザー アカウントの一覧が表示されます。 Christie Cline は会社内の新しい役割に異動し、Microsoft 365 パイロット プロジェクトにはもう在籍していないため、**Microsoft 365 E5** ライセンスの彼女のアカウントへの割り当てを解除して、Holly Dickson の新しいアカウントにそれらを再割り当てできるようにします。

5. **[アクティブなユーザー]** ページ上のユーザー一覧内で "**Christie Cline**" を選択します (名前の横にあるチェック ボックスではなく、ハイパーリンクされた Christie の名前を選択します)。

6. 表示される **[Christie Cline]** ペイン内には、**[アカウント]** タブが既定で表示されます。 **[ライセンスとアプリ]** タブを選択します。**[ライセンス (2)]** の下で、**[Microsoft 365 E5]** の横にあるチェック ボックスを選択してクリアし、**[変更の保存]** を選択します。 変更が保存されたら、**[Christie Cline]** のペインを閉じます。

7. これで、Adatum 社の新しい Microsoft 365 管理者である Holly Dickson 用のユーザー アカウントを作成する準備ができました。 そうすることで、Holly に Microsoft 365 グローバル管理者ロールを割り当て、Microsoft オンライン サービス全体のほとんどの管理機能とデータに対する、グローバルなアクセスを Holly に付与します。 Christie Cline から割り当てを解除したばかりの 2 つのライセンスも Holly に割り当てます。 <br/>

    **[アクティブなユーザー]** ウィンドウ内で、アクティブなユーザー一覧の上にあるメニュー バー上に表示されている **[ユーザーの追加]** オプションを選択します。 これで、**ユーザーを追加**ウィザードが起動します。

8. **ユーザーを追加**ウィザードの **[基本設定]** ページ内で、次の情報を入力します。

    - 名:**Holly**

    - 姓:**Dickson** 

    - 表示名:このフィールドに Tab キーで移動すると "**Holly Dickson**" と表示されます。

    - ユーザー名:**Holly** <br/>
    
        ‎**重要:****[ユーザー名]** フィールドの右側に [ドメイン] フィールドがあります。 "**xxxxxZZZZZZ.onmicrosoft.com**" クラウド ドメインが事前に入力されます (xxxxxZZZZZZ はラボ ホスティング プロバイダーから提供されたテナントのプレフィックス)。<br/>
    
    - **[パスワードを自動作成する]** チェック ボックスをクリアする (オフにする) と新しいフィールドが表示されるので、ここに管理者が定義したパスワードを入力します。

    - 表示された新しい **[パスワード]** フィールド内に、テナント管理者アカウント (つまり MOD 管理者アカウント) 用にラボ ホスティング プロバイダーから提供されたものと同じ**管理パスワード**を入力します

    - **[初回サインイン時にこのユーザーにパスワードの変更を要求する]** チェックボックスをクリア (オフに) します 

9. [**次へ**] を選択します。 **パスワードの保存**ダイアログ ボックスがスクリーンの上部に表示される場合は、**[なし]** を選択します。

10. **[製品ライセンスの割り当て]** ページ内で次の情報を入力します。 <br/>

    - 場所を選択:**米国**

    - ライセンス:**[ユーザーに製品ライセンスを割り当てる]** オプションの下にある  **[Microsoft 365 E5]** のチェック ボックスをオンにします

11. [**次へ**] を選択します。

12. **[オプションの設定]** ページ内で、**[役割]** の右側にあるドロップダウン矢印を選択します。 

13. **[役割]** セクション内で、**[管理センターに対するアクセス許可]** オプションを選択します。 このオプションを選択すると、最も一般的に使用される Microsoft 365 管理者ロールがその下で有効になります。  <br/>

    **注:**  最後の一般的なロールに続いて表示される **[すべてをカテゴリ別に表示]** を選択すると、すべての管理者ロールが表示されます。 Holly の場合、一般的に使用されるロール一覧内に表示される [グローバル管理者] ロールを Holly に割り当てるため、すべての管理者ロールをカテゴリ別に表示する必要はありません。

14. **[グローバル管理者]** チェック ボックスをオンにします。 <br/>

    **注:**  Adatum 社には 7 人のグローバル管理者が既に存在することを示す警告メッセージが表示されます。 通常の環境であれば、これは多すぎるため推奨されません。 このラボの目的上、ラボ ホスティング プロバイダーは、MOD 管理者と、その他 6 個のユーザー アカウントにグローバル管理者ロールを割り当てました。これは通常、実際の展開では実施しません。 ただし、架空の Adatum 社のラボ環境におけるこのラボの目的上、このメッセージは無視してください。 **とはいえ、実際の Microsoft 365 の展開においては、グローバル管理者を 2 - 4 人にするというベスト プラクティス ガイドラインを遵守する必要があります。** 

15. [**次へ**] を選択します。

16. **[確認と完了]** ウィンドウ上で、選択内容を確認します。 変更が必要なものがあれば、適切な **[編集]** リンクを選択し、その必要な変更を加えます。 それ以外の場合 (すべてが正しい場合) は、**[追加の完了]** を選択します。 

17. **[Holly Dickson がアクティブなユーザーに追加されました]** ページ上の **[ユーザーの詳細]** セクションの下にある **[表示]** オプションを選択し、Holly のパスワードが、ラボ ホスティング プロバイダーから提供されたテナント管理者アカウント (つまり MOD 管理者アカウント) 用の**管理パスワード**と同じであることを確認します。  <br/>

    **注:**  誤って違うパスワードを入力した場合は、**[アクティブなユーザー]** ページに戻ってから**パスワードのリセット**アイコン (Holly のアカウントにマウス ポインターを置くと表示されるキー アイコン) を選択し、そのパスワードを正しい値に変更する必要があります。

18. **[閉じる]** を選択します。

19. 次のタスクのために、ブラウザー内で Microsoft 365 管理センターを開いた状態で、Client 1 VM (LON-CL1) にログインしたままにしてください。

### タスク 2 – Microsoft 365 パイロット プロジェクト グループに Holly を追加する

前のタスクを完了した後、**MOD 管理者**アカウントとして **Microsoft 365 管理センター**に引き続きサインインしている必要があります。 このタスクでは、Adatum 社の新しい Microsoft 365 管理者である Holly Dickson として、Adatum 社の Microsoft 365 パイロット プロジェクトの実装を開始します。 このため、MOD 管理者として Microsoft 365 からログアウトして、このタスクをはじめ、Holly としてログインし直します。 

前のタスクでは、Adatum 社のパイロット プロジェクト チームのメンバー用に Microsoft 365 グループを作成し、そのグループのカスタム テーマを作成できました。 このタスクでは、Holly をこのグループに追加します。 

1. LON-CL1 VM 上では、前のタスクから引き続き、Microsoft Edge ブラウザー内で **Microsoft 365 管理センター**が開かれているはずです。 **MOD 管理者**として Microsoft 365 にサインインする必要があります。 <br/>

    **[Microsoft 365 管理センター]** タブ上で、スクリーンの右上隅に MOD 管理者の名前とメガフォン アイコンが表示されていることに注目してください。 この名前は、前のラボ演習で作成したカスタム テーマ (MOD 管理者を含む Microsoft 365 パイロット プロジェクト ユーザーのグループに関連付けられたもの) によって表示されています。 Holly Dickson としてログインし直したら、この点を覚えておいてください。 <br/>

    ブラウザーの右上隅にある **MOD 管理者**のユーザー アイコンを選択します。 表示される **[MOD 管理者]** ウィンドウ内で、**[サインアウト]** を選択します。 <br/>
    
    **重要:** 1 つのユーザー アカウントからサインアウトして別のアカウントにサインインする際は、**[サインアウト]** タブ以外のブラウザー タブをすべて閉じる必要があります。これは、前のユーザーに関連のあるウィンドウを閉じることで混乱を避けるためのベスト プラクティスです。 MOD 管理者アカウントからサインアウトしたら、少し時間をおいてから **[サインアウト]** タブ以外のその他すべてのブラウザー タブを閉じます。 
    
2. Microsoft Edge ブラウザー内の **[サインアウト]** タブ内で、アドレス バーの中に次の URL を入力して Microsoft 365 にサインインし直します: **https://portal.office.com**。 

3. **[アカウントを選択する]** ウィンドウ内に、サインアウトしたばかりの MOD 管理者のテナント管理者アカウント (admin@xxxxxZZZZZZ.onmicrosoft.com アカウント) のみが表示されます。 **[別のアカウントを使用する]** を選択します。 

4. **[サインイン]** ウィンドウ内で、「**Holly@xxxxxZZZZZZ.onmicrosoft.com**」 (xxxxxZZZZZZ は、ラボ ホスティング プロバイダーから提供されたテナントのプレフィックス) と入力します。 [**次へ**] を選択します。

5. **[パスワードの入力]** ウィンドウ内で、ラボ ホスティング プロバイダーから提供され、Holly のアカウントにも割り当てたテナント管理者アカウント (MOD 管理者アカウント) と同じ**管理パスワード**を入力し、**[サインイン]** を選択します。 必要に応じて、MFA サインイン プロセスを実行します。  <br/>

    **注:**  この時点から、Holly と MOD 管理者は、ラボ ホスティング プロバイダーによって提供される**管理パスワード**が割り当てられている唯一のユーザーになります。 他のすべてのユーザーには、ラボ ホスティング プロバイダーによって提供される**ユーザー パスワード**が割り当てられます。

6. スクリーンの中央に **[Microsoft 365 へようこそ]** ダイアログ ボックスが表示された場合は、これを閉じるオプションはありません。 代わりに、ウィンドウの右側にある右方向矢印アイコン (**>**) を 2 回選択し、それからチェック マーク アイコンを選択して、このメッセージング ウィンドウ内のスライドを進みます。 

7. **[Create with Microsoft 365]** ウィンドウが表示された場合は、ウィンドウの右上隅にある **[X]** を選択して閉じます。 

8. **[Microsoft 365 へようこそ]** ページが、Edge ブラウザー内の **[ホーム|Microsoft 365]** タブ内に表示されます。これは Holly の Microsoft 365 ホーム ページです。 Holly のイニシャルがスクリーンの右上隅に表示されることに注目してください。ただし、Holly の名前は表示されません。 これは、前のラボ演習の中でカスタム テーマに関連付けられたグループに Microsoft 365 パイロット プロジェクト ユーザーを追加した時点で、Holly のアカウントが存在しなかったためです。 Holly はシステムにログインする際に、各 Microsoft 365 ウィンドウの上部に自分の名前を表示するために、まず Microsoft 365 パイロット プロジェクト ユーザーのグループに自分のアカウントを追加したいと考えています。 <br>

    スクリーンの一番左端に表示されるアプリケーション アイコンの列の中で、**[管理]** を選択します。これで、新しいブラウザー タブ内に **Microsoft 365 管理センター**が開きます。 

9. **[Microsoft 365 管理センター]** の左側ナビゲーション ウィンドウ内で **[チームとグループ]** を選択し、その下にある **[アクティブなチームとグループ]** を選択します。 

10. **[アクティブなチームとグループ]** ページ内には、各グループの種類を表示するためのタブがあります。 既定では、**[Teams & Microsoft 365 グループ]** タブが表示されます。 このタブ内で、"**M365 パイロット プロジェクト**" を選択します。

11. 表示される **[M365 パイロット プロジェクト]** ペイン内では、**[全般]** タブが既定で表示されます。 **[メンバー]** タブを選択します。

12. **[メンバーシップ]** タブ内の **[所有者]** サブタブは、ペインの左側に表示されるナビゲーション ウィンドウ内に既定で表示されます。 その下に表示される **[メンバー]** サブタブを選択します。

13. **[メンバー]** サブタブ内で、**[+メンバーの追加]** を選択します。

14. 表示される **[M365 パイロット プロジェクト にチーム メンバーを追加する]** ペイン内で、**[名前またはメール アドレスで検索します]** フィールドの内部を選択します。 表示されるユーザー一覧内で、下にスクロールして "**Holly Dickson**" を選択します。 **[追加 (1)]** ボタンを選択し、Holly がグループに追加されたら、**[M365 パイロット プロジェクト にチーム メンバーを追加する]** ペインを閉じます。

15. **[アクティブなチームとグループ]** ページ上で、スクリーンの上部に表示される、アドレス バーの左側にある**更新**アイコンを選択します。 スクリーンの右上隅にあるイニシャルの横に Holly Dickson の名前がどう表示されるかに注目してください (注: Holly の名前を表示するには、2 回更新しなければならない場合があります)。

16. **[Microsoft 365 管理センター]** 内で、左側ナビゲーション ウィンドウ内の **[ユーザー]** を選択してから、その下にある **[アクティブなユーザー]** を選択します。

17. **[アクティブなユーザー]** ウィンドウ内で、ユーザーの**表示名**の上にマウス ポインターを置くと、そのユーザー名の右側に**キー アイコン**が表示されます。 そのキー アイコンを選択すると、ユーザーのパスワードをリセットすることができます。 Adele Vance、Alex Wilber、Joni Sherman、Lynne Robbins、Patti Fernandez のパスワードを、ラボ ホスティング プロバイダーからテナント管理者アカウント (つまり MOD 管理者アカウント) 用に提供されたもの (前に Holly Dickson に割り当てたもの) と同じ**管理パスワード**にリセットする必要があります。<br/>

    **Adele Vance** の上にマウス ポインターを置き、表示されるキー アイコンを選択します。

18. Adele に表示される **[パスワードのリセット]** ペイン内で、**[パスワードを自動作成する]** チェック ボックスをクリア (オフに) します。 

19. 表示される **[パスワード]** フィールド内に、ラボ ホスティング プロバイダーからテナント管理者アカウント (つまり MOD 管理者アカウント) 用に提供されたものと同じ**管理パスワード**を入力します。 **[パスワード]** フィールドの末尾にある目 (**パスワードの表示**) のアイコンを選択して、入力した値を表示します。 テナント パスワードが正しく入力されたことを確認します。

20. **[初回サインイン時にこのユーザーにパスワードの変更を要求する]** チェックボックスをクリア (オフに) します。

21. **[パスワードのリセット]** を選択します。 スクリーンの上部に**パスワードの保存**ダイアログ ボックスが表示されたら、**[なし]** を選択します。 次に、**[パスワードがリセットされました]** ペイン上で **[閉じる]** を選択します。

22. **Alex Wilber**、**Joni Sherman**、**Lynne Robbins**、**Patti Fernandez** に対して、手順 17 から 21 を繰り返します。 それぞれのパスワードを、ラボ ホスティング プロバイダーからテナント管理者アカウント (つまり MOD 管理者アカウント) 用に提供されたものと同じ**管理パスワード**にリセットします。 手順 19 で、入力したパスワードを表示して、正しい値を確認することを忘れないでください。

23. 次のタスクのために、ブラウザー内で **Microsoft 365 管理センター**を開いた状態で、LON-CL1 にログインしたままにしてください。


### タスク 3:MFA を実装するための条件付きアクセス ポリシーを作成する

**重要:** このタスクは、すべてのユーザーに対して MFA を実装するために Microsoft が作成した条件付きアクセス ポリシーを調べることから始まります。 ただし、ラーニング パートナーは、最近の MFA ポリシーの変更よりも前の試用版テナントを使用している可能性があります。 各ユーザーのサインイン後に MFA の実行を要求されていない場合、その試用版テナントでは MFA は必要ありません。 この場合、Microsoft が作成した MFA ポリシーはポリシーの一覧に表示されません。 使用しているテナントがこれに該当する場合、このポリシーを確認する手順はスキップしてください。 

トレーニングで示したように、MFA を実装する方法は 3 つあります。条件付きアクセス ポリシー、セキュリティの既定値、従来のユーザーごとの MFA (大規模な組織には推奨されません) です。 この演習では、条件付きアクセス ポリシーを使用して MFA を有効にします。これは Microsoft が推奨する方法です。 Adatum 社では、内部ユーザーと外部ユーザーの両方で、すべての Microsoft 365 ユーザーに対して MFA を有効にするよう Holly に要請がありました。 ただし、Adatum 社の Microsoft 365 パイロット プロジェクトの実装をテストするために、Holly は M365 パイロット プロジェクト グループのメンバーに対しては MFA を使用したサインインを不要にしたいと考えています。 パイロット プロジェクトが完了したら、Holly はポリシーを更新して、MFA の要件からこのグループを対象外にする条件を削除します。 このポリシーには、その他 2 つの要件も含めます。 すべてのクラウド アプリで MFA が必要になり、たとえユーザーが信頼できる場所からサインインした場合でも MFA が必要になります。 

**注:**  このタスクでは MFA を有効にする条件付きアクセス ポリシーを作成しますが、有効にはしません。 一部の学生は、MFA を必要とするテナントに属している場合があります。その場合、このポリシーは適用されません。 また、クラスのすべての学生が MFA を必要としないテナントに属している場合であっても、ポリシーの有効化は行いません。 この演習のポイントは、MFA を有効にするポリシーを作成するエクスペリエンスを提供することであり、実際に MFA を使用して認証することではありません。これは、その方法を把握していることを前提としています。 そのため、クラス内の潜在的なテナントの状況を考慮した最善の妥協策として、学生がポリシーの有効化を行わないようにすることを選択しました。 

1. LON-CL1 VM 上では、前のタスクから引き続き、Microsoft Edge ブラウザー内で **Microsoft 365 管理センター**が開かれているはずです。 **Holly Dickson** として Microsoft 365 にサインインする必要があります。
   
2. **[Microsoft 365 管理センター]** 内で、ナビゲーション ウィンドウ内の **[管理センター]** セクションの下にある **[ID]** を選択します。 これにより、新しいブラウザー タブ内に [Microsoft Entra 管理センター] が開きます。**[アカウントを選択する]** ウィンドウが表示されたら、**Holly Dickson のアカウント**を選択します。

3. **[Microsoft Entra 管理センター]** 内で、ナビゲーション ウィンドウ内の **[保護]** を選択し、**[条件付きアクセス ]** を選択します。

4. **[条件付きアクセス | 概要]** ページ上で、中央のナビゲーション ウィンドウの **[ポリシー]** を選択します。

5.    **重要:**  各ユーザーのサインイン後に MFA の実行を要求されていない場合、その試用版テナントでは MFA は必要ありません。 この場合、**Microsoft パートナーとベンダーの多要素認証**という名前のポリシーはポリシーの一覧に表示されません。その場合は、手順 11 に進み、独自の条件付きアクセス ポリシーの作成を開始する必要があります。 

 **[条件付きアクセス | ポリシー]** ページ上で、ご利用の Microsoft 365 サブスクリプションで使用することができる既定のポリシーを確認します。 「**Microsoft パートナーとベンダーの多要素認証**」というタイトルのポリシーに注意してください。 これは、Microsoft が作成した条件付きアクセス ポリシーであり、すべてのクラウド アプリ上のすべてのユーザーに対して MFA を要求します。 この試用版テナント内のすべてのユーザーに対して Microsoft が MFA を適用する方法を確認するには、このポリシーを選択します。   <br/>



6. **[Microsoft パートナーとベンダーの多要素認証]** ページで、**[ユーザー]** グループの下にある **[すべてのユーザーが含まれ、特定のユーザーは除外される]** を選択します。 これにより、2 つのタブ (**[対象]** と **[対象外]**) が表示されます。

7. **[対象]** タブで、**[すべてのユーザー]** が選択されていることに注意してください。 好奇心を満たすために、MFA をオフにしてこのポリシーを変更してみましょう。 **[なし]** を選択し、**[保存]** ボタンを選択します。 <br/>

    **何が起きたかに注目してください。** ページの上部に、**Microsoft パートナーとベンダーの多要素認証の更新に失敗 **を示すメッセージ ボックスが一時的に表示されます。 その後、システムは **条件付きアクセス | ポリシー]** ページに戻りました。 このメッセージが表示されない場合は、この手順をもう一度繰り返します。  <br/>

    同じことが起こるのは、**[対象]** タブで **[ユーザーとグループ]** を選択し、すべてのユーザーではなく特定のユーザーまたはグループを選択した場合です。 実際、Microsoft はセキュリティ ファイアウォールを組み込み、このポリシーに変更を加えようとした場合、ポリシーを保存しようとすると失敗します。 

8. Microsoft は、このポリシーに 1 つの除外項目を組み込みました。 それでは、それを見てみましょう。 **[ポリシー]** ページで、**Microsoft パートナーとベンダーの多要素認証**ポリシーをもう一度選択し、**[すべてのユーザーが含まれ、特定のユーザーは除外される]** を選択します。 今回は、**[対象外]** タブを選択します。 

9. Microsoft が **[ディレクトリ ロール]** チェック ボックスをオンにしていることに注意してください。 このオプションの下にあるフィールドを選択します。 MFA から除外することを選択できるロールのメニューで、Microsoft が選択したロールは**ディレクトリ同期アカウント**のみです。 このロールは Microsoft Entra Connect Sync サービス アカウントに自動的に割り当てられ、それ以外の場合は使用されません。 ディレクトリ同期タスクを実行するアクセス許可のみを持つ特別なロールです。 このロールは、ローカルの Active Directory Domain Services (AD DS) を Microsoft Entra ID に同期し、ID の共存を実現するために重要です。 同期サービスは MFA プロンプトによって引き起こされる可能性のある中断なしに継続的に実行する必要があるため、このロールに対して MFA は必要ありません。 さらに、このサービス アカウントは非常に制限されたアクセス許可で構成されており、対話型サインインには使用されないため、セキュリティ リスクが軽減されます。   <br/>

    ユーザーまたは選択したユーザーを含めないように MFA 設定を変更しようとした前の手順と同様に、MFA 設定を回避するために他のロールを選択しようとすると、ポリシーを保存しようとしたときに **Microsoft パートナーとベンダーの多要素認証の更新に失敗したこと**を示す同じエラーが発生します。 Microsoft のセキュリティ ファイアウォールでは、MFA を使用する必要があるユーザーに影響を与えるこの条件付きアクセス ポリシーを変更することはできません。

10. **Microsoft パートナーとベンダーの多要素認証**ページが開いている場合は、右上隅にある **X** を選択して閉じ、**[条件付きアクセス | ポリシー]** ページに戻ります。 または、ポリシーの変更を保存しようとした場合、試行は失敗し、既に **[条件付きアクセス | ポリシー]** ページに戻っているはずです。

11. **[条件付きアクセスの場合 | ポリシー]** ページの上部にあるメニュー バーで、**[+ 新しいポリシー]** を選択します。

12. **[新規] [条件付きアクセス ポリシー]** ウィンドウ上で、**[名前]** フィールド内に「**MFA for all Microsoft 365 users**」と入力します。

13. まず、ユーザーに対する MFA 要件を定義します。 **[ユーザー]** のグループの下にある、**[0 個のユーザーとグループが選択されました]** を選択します。 これにより、2 つのタブ (**[対象]** と **[対象外]**) が表示されます。

14. **[対象]** タブの下にある **[すべてのユーザー]** を選択します。 表示される警告メッセージに注意してください。 これについては、次の 2 つの手順で対処します。

15. **[対象外]** タブを選択します。システム ロックアウトを回避するには、前の警告メッセージが示したように、グローバル管理者 (この場合は Holly) を対象外にする必要があります。 Holly はテスト時の利便性を考慮して、他の Microsoft 365 パイロット プロジェクト グループ メンバーも対象外にしたいと考えています。 Microsoft 365 の運用が開始されたら、Holly はこの条件付きアクセス ポリシー内の対象外一覧からパイロット プロジェクト グループを削除し、自分自身とその他数人のグローバル管理者だけを対象外にします。 しかし現時点では、Holly はこのグループ全体を対象外にしたいと考えています。 <br/>

    これを行うには、**[ユーザーとグループ]** を選択します。 

16. 表示される **[除外されたユーザーとグループの選択]** ウィンドウ上で、"Microsoft 365 パイロット プロジェクト" グループを選択します。 **[すべて]** タブは既定で表示されます。 パイロット プロジェクト グループをすばやく見つけるには、**[グループ]** タブを選択します。アクティブなグループの一覧内で、"**M365 パイロット プロジェクト**" グループの横にあるチェック ボックスをオンにし、ウィンドウの下部にある **[選択]** ボタンを選択します。 **[新規] [条件付きアクセス ポリシー]** ウィンドウに戻り、**[ユーザー]** セクションの下に表示されるメッセージに注目してください。 

17. 次に、すべてのクラウド アプリに対する MFA 要件を定義します。 **[ターゲット リソース]** セクションの下で、**[ターゲット リソースが選択されていません]** を選択します。 これにより、2 つのタブ (**[対象]** と **[対象外]**) が表示されます。

18. **[このポリシーが適用される内容を選択]** ドロップダウン フィールドを選択して、ドロップダウン メニューのさまざまなオプションを表示します。 **[クラウド アプリ]** を選択します。 

19. **[対象]** タブの下で、既定の設定が **[なし]** であることに注目してください。 この設定を変更しない場合、クラウド アプリでは MFA が不要になります。これには Microsoft 365 が含まれます。 そのため、このポリシーを作成して、すべてのユーザーに対して MFA を要求とするオプションを選択したにもかかわらず、この **[ターゲット リソース]** の設定を **[なし]** のままにすると、Microsoft 365 にサインインするすべてのユーザーに対して MFA の使用が不要になります。 <br/>

    **[対象]** タブの下で、**[アプリの選択]** オプションを選択します。 これにより、**[フィルターの編集]** と **[選択]** の 2 つのセクションが表示されます。 **[選択]** の下で、**[なし]** を選択します。 表示される **[選択] [クラウド アプリ]** ペイン内で、アプリの一覧を下にスクロールして、MFA が必要になる可能性のある、さまざまなアプリをすべて表示します。 **どのアプリも選択しないでください。** ここでは、MFA を特定のアプリに制限すると決めた場合に、MFA を必要にするとどれだけ細かく設定することができるかを把握してもらうためだけにこの一覧をスクロールしています。  <br/>

    Adatum 社の場合、Holly はすべてのクラウド アプリで MFA を必要にしたいと考えています。特定のアプリを選択するよりも、通常はこれが一般的なビジネス シナリオです。 **[対象]** タブの下で、**[すべてのクラウド アプリ]** オプションを選択します。 Adatum 社では、いずれのクラウド アプリも MFA 認証の対象外にはしません。 提供されるオプションを確認したい場合は、**[対象外]** タブを選択します。 基本的には、**[対象]** タブと同じように動作します。このタブは表示できますが、対象外のクラウド アプリは選択しないでください。 

20. 最後に、すべてのユーザー サインインの場所に対する MFA 要件を定義します。 一部のシナリオでは、ユーザーが信頼されていない場所からサインインした場合にのみ、組織が MFA を必要とすることがあります。 ただし、Adatum 社では場所に関係なく、すべての対象ユーザーのサインインに MFA を要求したいと考えています。 <br/>

    **[条件]** で、**[0 個の条件が選択されました]** を選択してください。 これにより、ポリシーがチェックする可能性のある条件の一覧が表示されます。 このラボの演習では、**[場所]** 条件の下にある **[未構成]** を選択します。 これにより、**[構成]** トグル スイッチと 2 つのタブ (**[対象]** と **[対象外]**) が表示されます。 現在、両方のタブが無効になっています。

21. **[構成]** トグル スイッチを **[はい]** に設定すると、それらの 2 つのタブが有効になります。 

22. **[対象]** タブの下で、**[任意のネットワークまたは場所]** が選択されていることを確認します (必要に応じてこれを選択します)。 **[対象外]** タブを選択します。組織が特定の IP アドレスまたはアドレス範囲を "信頼できる" と認識している場合は、ユーザーがそのいずれかの場所からサインインした場合に、MFA 要件を対象外にすることができます。 ただし、Adatum 社では場所に関係なく、すべてのユーザーのサインイン試行に MFA を要求したいと考えています。 これには、内部および外部ユーザー サインインの両方が含まれます。**[選択された場所]** オプションが選択されていることを確認し、**[選択]** セクションの下に **[なし]** と表示されていることを確認します。 [選択された場所] を指定しないというこの設定により、MFA の対象外になる場所がないことが保証されます。 

23. **[アクセス制御]** セクションの下の、**[許可]** グループの下にある、**[0 個のコントロールが選択されました]** を選択します。 これにより、**[許可]** ペインが表示されます。

24. 表示される **[許可]** ペイン内で、**[アクセス権の付与]** オプションが選択されていることを確認します (必要に応じてこれを選択します)。 **[多要素認証を要求する]** チェック ボックスをオンにします。 このポリシーで有効にすることができる他のすべてのアクセス制御に注目してください。 このポリシーでは MFA のみが必要になります。 **[許可]** ペインの下部にある **[選択]** ボタンを選択すると、このペインが閉じます。 

25. **重要:** この時点で、通常は **[ポリシーの有効化]** フィールドを **[オン]** に設定します。 ただし、一部の学生は MFA を必要としない以前の試用版テナントに属しており、他の学生は MFA を必要とする新しいテナントに属している可能性があるため、作成したポリシーの有効化は行いません。 そのため、**[ポリシーの有効化]** フィールドを **[オフ]** に設定します。

27. **[作成]** ボタンを選択してこのポリシーを作成します。

28. 表示される **[条件付きアクセス | ポリシー]** ウィンドウ上で、"**MFA for all Microsoft 365 users**" のポリシーが表示され、その **[状態]** が **[オフ]** に設定されていることを確認します。

29. 次のタスクのために、すべての Microsoft Edge ブラウザー タブを開いた状態で、LON-CL1 にログインしたままにしてください。

**注:**  前述のように、MFA を必要とする Microsoft 365 試用版テナントを使用している場合、条件付きアクセス ポリシーをテストする方法はありません。 Microsoft の条件付きアクセス ポリシーでは、すべてのユーザーに MFA を要求します。 MFA を要求する複数のポリシーがある場合は、最も制限の厳しいポリシーが適用されます。 この場合、Microsoft のポリシーは、パイロット プロジェクト グループ メンバーの例外を含む先ほど作成したポリシーよりも制限が厳しくなっています。そのため、ポリシーをテストする方法はありません。 MFA を必要としない以前のテナントの場合は、クラス内の他の学生が MFA の使用を必要とするテナントに既に属している可能性があるため、そのテストは行いません。 他のユーザーがテストできない状況でポリシーをテストするのではなく、ポリシーをテストしないことを選択しました。 この試用版テナントを使用してポリシーをテストすることはできませんが、このエクスペリエンスを使用して条件付きアクセス ポリシーを作成し、実際の Microsoft 365 展開で MFA を要求することをおすすめします。


### タスク 4:Microsoft Entra スマート ロックアウトを展開する

Adatum 社の CTO から、Microsoft Entra スマート ロックアウトを展開するよう要請されました。これは、ユーザーのパスワードを推測する、またはブルート フォース方式を使用するなど、ネットワークに侵入しようとする悪意のあるアクターをロックアウトするのに役立ちます。 スマート ロックアウトは、有効なユーザーからのサインインを認識し、攻撃者や他の未知のソースからのサインインとは異なる方法で処理できます。 

CTO は、スマート ロックアウトの実装を希望しています。Adatum のユーザーが引き続き自分のアカウントにアクセスして生産性を維持できるようにする一方、攻撃者をロックアウトするためです。 ユーザーが同じパスワードを複数回使用することができないように、また、単純すぎたり一般的だと思われるパスワードを使用することができないようにスマート ロックアウトを構成するよう、 CTO から Holly に要請がありました。 

**注:**  アカウント ロックアウト ポリシーの設定は、グループ ポリシー管理エディターと Microsoft Entra 内の両方で、スマート ロックアウト機能を使用してメンテナンスすることができます。 このラボ タスクではそれぞれの方法にどうアクセスするかを説明しますが、実施するのは Microsoft Entra 内のスマート ロックアウト設定の更新のみです。 グループ ポリシー管理エディターにアクセスするには、会社のドメイン コントローラー (LON-DC1) を使用する必要があります。 

1. 前のタスクでは、LON-CL1 内で作業しました。 このタスクでは、Adatum 社のドメイン コントローラーである LON-DC1 から作業します。 <br/>

    **LON-DC1** に切り替えます。

2. **LON-DC1** 上では、**Ctrl + Alt + Delete** キーを押してログインする必要があります (VM 環境内でこのオプションを見つける方法については、講師が説明します)。 ラボ ホスティング プロバイダー (**管理者**) がパスワード **Pa55w.rd** を使用して作成したローカル Adatum 管理者アカウントとして、LON-DC1 にログインします。

3. LON-DC1 上では、起動時に**サーバー マネージャー**が自動的に開始されます。 **[サーバー マネージャー]** 内で、右上にあるメニューバー内の **[ツール]** を選択し、ドロップダウン メニュー内で **[Group Policy Management]** を選択します。 表示される **[Group Policy Management]** ウィンドウを最大化します。

4. 所属組織のアカウント ロックアウト ポリシーが含まれているグループ ポリシーを編集してください。 必要に応じて、左側ペイン内のルートのコンソール ツリー内で、**[フォレスト:Adatum.com]**、**[ドメイン]**、**[Adatum.com]** の順に展開します。  <br/>

    **[Adatum.com]** の下で、**[Default Domain Policy]** を右クリックし、メニュー内の **[編集]** を選択します。

5. 表示される **[グループ ポリシー管理エディター]** ウィンドウを最大化します。

6. 左側ペイン内の **[Default Domain Policy]** ツリー内で、**[コンピューターの構成]** の下にある **[ポリシー]**、**[Windows の設定]**、**[セキュリティ設定]**、**[アカウント ポリシー]** の順に展開します。

7. **[アカウント ポリシー]** フォルダー内で **[アカウント ロックアウトのポリシー]** を選択します。

8. 右側のペインを見ればわかるように、スマート ロックアウトのパラメーターは定義されていません。 グループ ポリシー管理エディター内でこれらのロックアウト パラメーターをメンテナンスする代わりに、Microsoft Entra 管理センターを使用します。 グループ ポリシー管理エディターを使用することもできますが、この方法は通常、オンプレミスの Active Directory 環境内で使用されます。 このエディターについて説明したのは、この代替方法を確認してもらうためです。 ただし、Microsoft 365 のようなクラウドベースのサービスを厳密に使用している組織や、グループ ポリシー管理エディターにアクセスするよりも Microsoft Entra 管理センターを使用するうほうがはるかに使いやすいと認識している組織には、**Microsoft Entra 管理センター**を使用して、Entra ID コンテキスト内に対応する値を割り当てることをお勧めします。 <br/>  

    ロックアウトの動作とカスタマイズのオプションは、2 つの方法で異なることも覚えておいてください。 グループ ポリシー管理エディターを使用すると、アカウント ロックアウトのしきい値、ロックアウト期間、ロックアウト カウンターのリセットなど、ポリシー設定をより細かく制御することができます。 ただし、この方法を使用するには、グループ ポリシーと Active Directory 管理について熟知している必要があります。 逆に、Microsoft Entra 内のアカウント ロックアウト ポリシーは、広範囲にカスタマイズすることはできません。 ただし、グループ ポリシーでは使用することができる微調整のオプションの一部はありませんが、より使いやすくなっています。 <br/>

    Adatum 社の場合、Holly は Microsoft Entra 管理センターを使用して会社のアカウント ロックアウト ポリシーを構成することを選択しました。 スクリーンの下部にあるタスクバー上で **Microsoft Edge** アイコンを選択します。 ブラウザー ウィンドウが開いたら、必要に応じて最大化します。

9. Edge ブラウザー内で、アドレス バー内に次の URL を入力して、**Microsoft 365 ホーム** ページに移動します: **https://portal.office.com** 

10. **[サインイン]** ダイアログ ボックス内で、Holly Dickson としてサインインする必要があります。 「**Holly@xxxxxZZZZZZ.onmicrosoft.com**」と入力します。xxxxxZZZZZZ はラボ ホスティング プロバイダーから割り当てられたテナントのプレフィックスです。 [**次へ**] を選択します。 <br/>

11. **[パスワードの入力]** ダイアログ ボックス内で、ラボ ホスティング プロバイダーから提供された一意の**管理パスワード**を入力し、**[サインイン]** を選択します。 必要に応じて、MFA サインイン プロセスを実行します。

12. **[サインインの状態を維持しますか?]** ダイアログボックス上で、**[今後、このメッセージを表示しない]** チェックボックスをオンにして、**[はい]** を選択します。 表示される**パスワードの保存**ダイアログ ボックス上で、**[なし]** を選択します。

13. スクリーンの中央に **[Microsoft 365 へようこそ]** ダイアログ ボックスが表示された場合は、これを閉じるオプションはありません。 代わりに、ウィンドウの右側にある右方向矢印アイコン (**>**) を 2 回選択し、それからチェック マーク アイコンを選択して、このメッセージング ウィンドウ内のスライドを進みます。 

14. **[Find more apps]** ウィンドウまたは **[Create with Microsoft 365]** ウィンドウが表示される場合は、ウィンドウの右上隅にある **[X]** を選択して閉じます。 

15. **[Microsoft 365 へようこそ]** ページ上で、左側のペイン内に表示されるアプリケーション アイコンの一覧の中で **[管理]** を選択します。これで、新しいブラウザー タブ内に **[Microsoft 365 管理センター]** が開きます。 

16. **Microsoft 365 管理センター**のナビゲーション ウィンドウで、**[すべて表示]** を選択します。 **[管理センター]** の下にある **[ID]** を選択すると、**[Microsoft Entra 管理センター]** が新しいタブ内に表示されます。

17. **[Microsoft Entra 管理センター]** 内で、ナビゲーション ウィンドウ内の **[保護]** を選択し、**[認証方法]** を選択します。

18. **[認証方法]、[ポリシー]** ページの **[管理]** セクションの中央のウィンドウで **[パスワード保護]** を選択します。

19. **[認証方法]、[パスワード保護]** ウィンドウの右側にある詳細ウィンドウで以下の情報を入力します。

    - **[カスタム スマート ロックアウト]** セクション:

        - **[ロックアウトしきい値]**: このフィールドは、最初のロックアウト前に、アカウントのサインイン失敗が何回まで許可されるのかを示します。 既定値は 10 です。 テスト目的で、Adatum 社ではこれを「**3**」に設定するように要求しました。

        - **[ロックアウト期間 (秒)]:** これは各ロックアウトの時間 (秒数) です。 既定値は 60 秒 (1 分) です。 Adatum 社ではこれを「**90**」秒に変更するように要求しました。

    - **[カスタム禁止パスワード]** セクション:

        - **[カスタム リストの強制]**: **[はい]** を選択します。

        - **カスタムの禁止パスワードの一覧**:以下の値を入力します (各値の入力後に Enter を押して、各値が別個のラインになるようにしてください):

            - **Password01**

            - **F00tball01**

            - **Se@Hawks1**

            - **Never4get!!**

    - **[モード]** セクション内で、**[強制]** を選択します

20. ページ最上部のメニュー バー上で **[保存]** を選択します。

21. これで禁止パスワードの機能をテストできます。 スクリーンの右上隅で Holly Dicksons のユーザー アイコンを選択し、表示されるメニュー内で **[アカウントを表示]** を選択します。 

22. 表示される **[マイ アカウント]** ウィンドウ内の、**[パスワード]** タイル内で、**[パスワードの変更]** を選択します。

23. 新しいタブが開き、**[パスワードの変更]** ウィンドウが表示されます。 **[古いパスワード]** フィールド内に、Holly の既存パスワードを入力します。これは、ラボ ホスティング プロバイダーからテナント管理者アカウント (つまり MOD 管理者アカウント) 用に提供された**管理パスワード**と同じです。 <br/>

    「**Never4get!!**」を **[新しいパスワードの作成]** と **[新しいパスワードの確認]** フィールド内に入力して、**[送信]** を選択します。 表示されるエラー メッセージに留意してください。

24. ブラウザー内で、**[パスワードの変更]** タブを閉じます。 

25. これでロックアウトしきい値の機能をテストできます。 スクリーンの右上隅にある "Holly Dicksons" のユーザー アイコンを選択し、表示されるメニュー内で **[サインアウト]** を選択します。  

26. Holly としてサインアウトすると、**[アカウントを選択する]** ウィンドウが **[Microsoft Entra にサインインする]** タブ内に表示されます。あるユーザーとして Microsoft オンライン サービスからサインアウトし、別のユーザーとしてサインインし直す場合は、ベスト プラクティスとして、**[サインアウト]** または **[サインイン]** タブを除くすべてのブラウザー タブを閉じてください。この場合は他のタブを今すぐ閉じて、**[サインイン]** タブを開いたままにします。  <br/>

    **[アカウントを選択する]** ウィンドウ内で、**[別のアカウントを使用する]** を選択します。 

27. **[サインイン]** ウィンドウ内で、Patti Fernandez としてサインインします。 「**pattif@xxxxxZZZZZZ.onmicrosoft.com**」 (xxxxxZZZZZZ はラボ ホスティング プロバイダーから提供されたテナントのプレフィックス) と入力してから **[次へ]** を選択します。 

28. **[パスワードの入力]** ウィンドウ上で、文字と数字を任意のランダムな組み合わせで入力し、**[サインイン]** を選択します。 表示される無効なパスワードのエラー メッセージに注目してください。 

    このステップをあと 2 回繰り返します。 
    
    **ロックアウトのしきい値**を **3** に設定したため、3 回目のサインイン試行失敗後に、このアカウントがロックされていることを示すエラー メッセージが表示されます。 <br/>

    **注:**  3 回目の試行後にこのロックアウト メッセージが表示されない場合は、このロックアウトしきい値変更のサービス全体に対する反映を、システムがまだ完了していません。 変更が反映されるまで数分かかる場合があります。 数分待ってから、誤ったパスワードを使用してもう一度サインインします。 このラボのテストでは、さまざまな結果が見られました。 場合によっては、この変更がほぼ即座に反映されて、3 回目のサインイン試行後にロックアウトされます。 それ以外の場合には、ロックアウト メッセージが表示されるまでに 5 分から 10 分かかりました。 ロックアウト メッセージが表示されるまで、このプロセスを続行してください。その時点で Patti のアカウントは一時的にロックされて、未承認のアクセスを防ぐことになります。

29. 前に設定した **90 秒のロックアウト期間**が過ぎるまで、Patti としてもう一度ログインすることはできません。 <br/>

    ロックアウトされたら、90 秒待ってから **pattif@xxxxxZZZZZZ.onmicrosoft.com** (xxxxxZZZZZZ はラボ ホスティング プロバイダーから割り当てられたテナントのプレフィックス) としてサインインし直します。 **[パスワード]** フィールドに、Patti のパスワードを入力します。これは、ラボ ホスティング プロバイダーによって提供される**ユーザー パスワード**です。 必要に応じて、MFA サインイン プロセスを実行します。 Patti として正常にサインインできることを確認します。

30. 正常にログインしたら、開いているすべてのアプリケーションを閉じてください。 これは、LON-DC1 ドメイン コントローラーを使用した最後のラボ演習になります。
 
# ラボ 2 - 演習 2 に進む
