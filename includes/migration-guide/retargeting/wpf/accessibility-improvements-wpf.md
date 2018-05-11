### <a name="accessibility-improvements-in-wpf"></a>WPF でのアクセシビリティの向上

|   |   |
|---|---|
|説明|<strong>ハイ コントラストの改善</strong></br><ul><li><xref:System.Windows.Controls.Expander> コントロールにフォーカスを合わせると、表示されるようになりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</li><li><xref:System.Windows.Controls.CheckBox> および <xref:System.Windows.Controls.RadioButton> コントロールを選択したとき、コントロールのテキストが .NET Framework の以前のバージョンより見やすくなりました。</li><li>無効になっている <xref:System.Windows.Controls.ComboBox> の境界が、無効なテキストと同じ色になりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</li><li>無効になっているボタンにフォーカスを合わせたとき、正しいテーマ色が使われるようになりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</li><li><xref:System.Windows.Controls.ComboBox> コントロールのスタイルが <xref:System.Windows.Controls.ToolBar.ComboBoxStyleKey?displayProperty=nameWithType> に設定されているとき、ドロップダウン ボタンが表示されるようになりました。 .NET Framework の以前のバージョンでは、表示されませんでした。</li><li><xref:System.Windows.Controls.DataGrid> コントロールの並べ替えインジケーターの矢印で、テーマの色が使われるようになりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</li><li>ハイパーリンクの既定のスタイルが、マウスでポイントされると正しいテーマの色に変わるようになりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</li><li>ラジオ ボタンに対するキーボード フォーカスが表示されるようになりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</li><li><xref:System.Windows.Controls.DataGrid> コントロールのチェック ボックス列で、キーボード フォーカスのフィードバックに予期される色が使われるようになりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</li><li><xref:System.Windows.Controls.ComboBox> および <xref:System.Windows.Controls.ListBox> コントロールで、キーボード フォーカスのビジュアルが表示されるようになりました。 .NET Framework の以前のバージョンでは、そうではありませんでした。</p></li></ul><strong>スクリーン リーダーの操作性の向上</strong></br><ul><li><xref:System.Windows.Controls.Expander> コントロールが、スクリーン リーダーによってグループ (展開/折りたたみ) として正しく読み上げられるようになりました。</li><li><xref:System.Windows.Controls.DataGridCell> コントロールが、スクリーン リーダーによってデータ グリッド セル (ローカライズ済み) として正しく読み上げられるようになりました。</li><li>スクリーン リーダーが、編集可能な <xref:System.Windows.Controls.ComboBox> の名前を読み上げるようになりました。</li><li><xref:System.Windows.Controls.PasswordBox> コントロールが、スクリーン リーダーによって &quot;ビューに項目がありません&quot; と読み上げられなくなりました。</p></li></ul><strong>LiveRegion のサポート</strong></br>ナレーターなどのスクリーン リーダーは、アプリケーションの UI の内容をユーザーに伝えるとき、通常は、現在フォーカスが設定されている UI について説明します。これは、おそらくそれがユーザーにとって最も関心のある要素であるためです。 しかし、画面内のどこかの UI 要素が変わり、フォーカスがなくなった場合、ユーザーに通知されず、重要な情報を逃すことがあります。 LiveRegions は、この問題を解決するためのものです。 開発者はこれを利用して、UI 要素が大幅に変更されたことをスクリーン リーダーやその他の [UI オートメーション](~/docs/framework/ui-automation/ui-automation-overview.md) クライアントに伝えることができます。 その後、スクリーン リーダーでは、その変更をユーザーに通知する方法とタイミングが決定されます。LiveSetting プロパティを使うと、UI に行われた変更をユーザーに通知するのがどの程度重要かをスクリーン リーダーに知らせることもできます。|
|提案される解決策|<strong>これらの変更を選択する方法と選択しない方法</strong></br>アプリケーションでこれらの変更を利用するには、.NET Framework 4.7.1 以降で実行する必要があります。 アプリケーションは、次のいずれかの方法でこれらの変更を利用できます。<ul><li>.NET Framework 4.7.1 を対象とします。 この方法をお勧めします。 .NET Framework 4.7.1 以降を対象とする WPF アプリケーションでは、これらのアクセシビリティの変更が既定で有効になります。</li><li>下の例のように、アプリ構成ファイルの <code>&lt;runtime&gt;</code> セクションで次の [AppContext スイッチ](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)を追加し、それを <code>false</code> に設定することで、以前のアクセシビリティ動作を無効にします。</li></ul><pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>.NET Framework 4.7.1 以降を対象とするアプリケーションで以前のアクセシビリティ動作を残す場合、この AppContext スイッチを明示的に <code>true</code> に設定することで以前のアクセシビリティ機能を選択できます。</br>UI オートメーションの概要については、「[UI オートメーションの概要](~/docs/framework/ui-automation/ui-automation-overview.md)」を参照してください。|
|スコープ|Major|
|Version|4.7.1|
|型|再ターゲット中|
|影響を受ける API|<ul><li><xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType></li><li><xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType></li><li><xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType></li><li><xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType></li><li><xref:System.Windows.Automation.AutomationProperties.SetLiveSetting(System.Windows.DependencyObject,System.Windows.Automation.AutomationLiveSetting)?displayProperty=nameWithType></li><li><xref:System.Windows.Automation.AutomationProperties.GetLiveSetting(System.Windows.DependencyObject)?displayProperty=nameWithType></li><li><xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore?displayProperty=nameWithType></li></ul>|
