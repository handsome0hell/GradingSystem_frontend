<template>
  <div class="home">
    <div
      class="container"
      v-loading="loading"
      element-loading-text="文件解析中"
      element-loading-spinner="el-icon-loading"
      element-loading-background="rgba(0, 0, 0, 0.1)"
    >
      <div class="addZujian"></div>
      <div class="zujianContent">
        <br />
        <!-- Vue提供了 component ,来展示对应名称的组件 -->
        <!-- component 是一个占位符, :is 属性,可以用来指定要展示的组件的名称 -->
        <component
          v-for="(item, index) in comName"
          :is="item.name"
          :key="item.id"
          :idx="index"
          @func="getContent(index)"
          @fromSubAddFileInfo="saveFile"
          @fromSubAddFileRemove="removeFile"
        >
        </component>
      </div>
      <div style="float: left; display: inline-block">
        <el-button type="primary" class="zujianBtn" @click="zujian"
          ><i class="el-icon-circle-plus-outline"></i> 新增项目</el-button
        >
      </div>

      <div
        style="float: right; display: inline-block"
        v-if="fileList.length > 0"
      >
        <el-checkbox v-model="isAgree">同意并接受</el-checkbox>
        <el-link type="primary" @click="showDialog()" style="font-size: 18px"
          >元智能科创项目评价系统服务协议</el-link
        >
        <el-dialog
          title=""
          :visible.sync="dialogVisible"
          width="600px"
          custom-class="userDig"
        >
          <div class="userAgree" style="height: 370px; overflow: auto">
            <span class="userAgree_txt">
              远见元智能科创项目评价系统服务协议 1.协议条款的确认和接纳
              1.1欢迎注册、登录平台（以下简称“本平台”或“科创项目评价系统”）、使用平台服务（以下简称“本服务”或“服务”），请您仔细阅读以下全部内容。本协议是您与科创项目评价系统之间关于服务的条款，内容包括本协议正文、本协议明确援引的其他协议及已经发布的或将来可能发布的各类协议和规则。所有协议内容为本协议不可分割的组成部分，与本协议正文具有同等法律效力。除另行明确声明外，您使用服务的行为将受本协议约束。
              1.2如您选择“点击同意”本协议或者以其他方式开始使用服务，即表示已经与本平台达成协议，并自愿接受本协议的所有内容。您确认，您应当具备中华人民共和国法律规定的与您行为相适应的民事行为能力，确保有能力对您使用本公司提供服务的一切行为独立承担责任。若您不具备前述主体资格或您是未满十八周岁的未成年人，请在您的监护人的陪同下阅读本服务条款，并在取得他们对您使用服务的行为以及对本服务条款的同意之后，使用本服务；本公司在依据法律规定或本协议约定要求您承担责任时，有权向您的监护人追偿。
              1.3本平台有权根据法律规范及运营的合理需要，不断修改和完善本协议，并在本平台公告。如您继续使用服务，即意味着同意并自愿遵守修改后的协议条款，抑或您有权终止使用。
              2. 定义
              2.1您：指注册帐号并经审核同意后，使用科创项目评价服务的用户。
              2.2本平台：远见元智能科创项目评价系统，是由南信大无锡研究院泛在服务计算研究所携旗下孵化企业远见（无锡）大数据科技有限公司与TSITE科技创新品牌联手推出的科创项目评价系统。
              2.3本公司：远见（无锡）大数据科技有限公司 3.帐号注册与使用
              3.1您可浏览本平台上的课程信息，如您希望使用本平台服务，您需先登录您的帐号，或注册本平台认可的帐号并登录。如您选用其他第三方帐号登录的，您应保证第三方帐号的稳定性、真实性以及可用性，如因第三方帐号原因（如第三方帐号被封号）致使您无法登录的，您应与第三方帐号的所属公司联系。您注册登录的帐号是确认您身份的唯一依据。
              您充分了解并同意，您必须为自己注册帐号下的一切行为负责，包括但不限于用户所发表的任何内容以及由此产生的任何后果。用户应对本服务中的内容自行加以判断，并承担因使用内容而引起的所有风险，包括因对内容的正确性、完整性或实用性的依赖而产生的风险。
              3.2注册完成后，请您妥善保存有关帐号和密码，并对该帐号进行的所有活动和行为负责。如因您自身原因（包括但不限于转让帐号、与他人共用、自己泄露等）或您所用计算机或其他终端产品感染病毒或木马，而导致帐号密码泄漏、遗失或其他损失后果将由您独自承担。
              3.3您在注册帐号时承诺遵守法律法规、社会主义制度、国家利益、公民合法权益、公共秩序、社会道德风尚和信息真实性七条底线，不得在帐号注册资料中出现违法和不良信息。
              3.4本平台有权对您提供的帐号注册资料进行审查，若发现或者收到举报确认注册资料存在不准确、不真实，或含有违法、不良信息，有权不予注册，并保留终止您使用本平台的权利。若您以虚假信息骗取帐号注册或帐号注册资料存在侵权、违法和不良信息的，本平台有权采取通知限期改正、暂停使用、注销登记等措施。对于冒用其他机构或他人名义注册帐号名称的，本平台有权注销该帐号，并向政府主管部门进行报告。
              3.5根据相关法律、法规规定以及考虑到产品服务的重要性，您同意：
              （1）在注册帐号时及时验证邮箱成为正式用户；
              （2）提供及时、详尽及准确的账户注册资料；
              （3）不得以营利、任何不正当手段或以违反诚实信用原则等为自己或他人开通、使用本服务；
              （4）用户对其自身帐号中的所有行为和事件负全责，不得售卖、转借帐号，不得私自进行帐号的交易等交易活动。
              如出现以上任何行为之一的，本平台将按照本服务条款要求用户承担相应的违约责任，如因此导致用户无法继续使用相关服务的，用户应当自行承担后果。
              3.6您若发现自身帐号或密码被他人非法使用或有登录、使用异常情况的，应及时通知本平台，本平台将按照本协议或法律规定进行处理。
              3.7您应当通过官方提供的正当合法途径付费以获得付费服务，其他非官方途径付费充值的，均不享受本公司保护，如发现用户未支付官网对价或未通过官网途径获取服务的，本公司有权限制、中止或终止用户帐号的登录和使用，停止向用户提供服务，本公司无需向用户退还已支付的任何费用。
              3.8您了解并同意，本平台可能会基于自身原因不定期的对付费服务内容或功能进行更新而无需经过您的事先同意。
              4.数据
              在法律法规允许的范围内，用户同意帐号所有权，以及与注册、使用帐号相关的服务记录，包括但不限于所有注册、登录、消费记录和相关的使用统计数据，归本公司所有。除非另有证明，本平台储存在其服务器上的数据是您使用服务的唯一有效证据。
              5.使用规则
              5.1您不得利用本平台制作、复制、发布、传播如下法律、法规和政策禁止
              的内容： 5.1.1反对宪法所确定的基本原则的；
              5.1.2危害国家安全，泄露国家秘密，颠覆国家政权，破坏国家统一的；
              5.1.3损害国家荣誉和利益的；
              5.1.4煽动民族仇恨、民族歧视，破坏民族团结的；
              5.1.5破坏国家宗教政策，宣扬邪教和封建迷信的；
              5.1.6散布谣言，扰乱社会秩序，破坏社会稳定的；
              5.1.7散布淫秽、色情、赌博、暴力、凶杀、恐怖或者教唆犯罪的；
              5.1.8侮辱或者诽谤他人，侵害他人合法权益的；
              5.1.9煽动非法集会、结社、游行、示威、聚众扰乱社会秩序；
              5.1.10以非法民间组织名义活动的；
              5.1.11含有法律、法规和政策禁止的其他内容的信息。
              5.2您不得利用本平台制作、复制、发布、传播包括但不限于如下干扰平台的正常运营，以及侵犯其他主体或第三方合法权益的内容：
              5.2.1广告、骚扰、垃圾信息的；
              5.2.2涉及他人隐私、个人信息或资料的；
              5.2.3侵害他人名誉权、肖像权、知识产权、商业秘密等合法权利的；
              5.2.4强制、诱导其他用户关注、点击链接页面或分享信息的；
              5.2.5虚构事实、隐瞒真相以误导、欺骗他人的；
              5.2.6未经书面许可利用本平台为第三方进行推广的（包括但不限于加入第三方链接、广告等行为）；
              5.2.7未经书面许可使用插件、外挂或其他第三方工具、服务接入平台和相关系统；
              5.2.8利用本平台从事任何违法犯罪活动的；
              5.2.9制作、发布与以上行为相关的方法、工具，或对此类方法、工具进行运营或传播，无论这些行为是否为商业目的；
              5.2.10 其他违反法律法规规定或干扰平台正常运营的行为。
              5.3您了解并同意，本平台有权应有权部门的要求，向其提供您提交给或在使用服务中存储于服务器的必要信息。如您涉嫌侵犯他人合法权益，则有权在初步判断涉嫌侵权行为存在的情况下，向权利人提供关于您的前述必要信息。
              5.4您知悉并同意，您购买的付费服务仅限于您自行使用，您无权对购买的收费课程及相关增值服务服务进行出售、转让、许可、传播或以其他方式使除您自己以外的第三方（包括但不限于自然人、法人或其他组织）使用。
              若您存在上述违规行为，本平台有权视您违反本协议行为的严重程度，对您采取以下单项或多项措施：
              5.4.1取消您继续使用该付费服务的权利
              5.4.2限制、暂停/终止提供全部或部分服务； 5.4.3删除违规内容；
              5.4.4要求您退还通过出售、转让、许可等其他方式取得的收益；
              5.4.5暂时/永久封禁帐号； 5.4.6其他采取的合理措施。
              如您因违规被暂停部分或全部服务，终止部分服务、被限制/中止帐号的登录和使用，对您已购买的服务费用，本公司将不予退回。如用户被终止全部服务或终止帐号登录的，无需向用户退还已支付的任何课程费用。
              5.5如果您违反本协议的行为给本平台或其他第三方造成损失的，您应当对此承担法律责任。您承担法律责任的形式包括但不限于：对受到侵害者进行赔偿；以及在本平台首先承担了因您的行为导致的行政处罚或侵权损害赔偿责任后，您应给予本平台等额的赔偿。若您账户内有剩余款项的，本平台有权不予退回，若不足以赔偿损失的，本平台仍有权要求您补足相应的损失。
              5.6如果您行使本协议规定的权利而购买/接受以外的第三方提供的内容或服务，如因此发生纠纷的，您应向销售/提供该内容或服务的第三方主张权利，与本平台无关。
              5.7对于在本平台上的内容,
              不保证其适用性或满足您特定需求及目的进行任何明示或者默示的担保。
              6.服务收费
              本平台项目评分服务免费提供，可能涉及其他付费服务，付费项目包括但不限于购买提供的付费评价服务以及其他增值服务服务。
              6.1您理解并同意：本平台提供的付费服务实行先付款后使用的方式，您及时、足额、合法的支付所需的款项是您获得该等服务的前提。您有权选择使用本平台认可的支付方式，您理解并确认支付服务由本平台之外具备合法资质的第三方提供，该等支付服务的使用条件及规范由您与支付服务提供方确定，与本平台无关。
              6.2如您选择购买付费服务，请您务必仔细了解本协议及确认相关具体信息，并根据操作提示，确认自己的帐号并选择相关操作选项。发布的付费服务可能对使用的时间、次数等做出一定限制；如超出限制范围，可能影响您继续使用该等服务，您需要再次付费购买。一经购买，即视为您认可该项服务标明之价格；您购买成功后，该项服务即时生效。本公司可能会根据服务的整体规划，对服务相关权益细则、收费标准、方式等进行修改和变更，前述修改、变更，本将在相应服务页面进行展示。
              6.3本公司不对所提供的付费项目的适用性或满足用户特定需求及目的进行任何明示或者默示的担保。您在购买前应确认自身的需求，同时仔细查阅相关介绍、说明。
              7.隐私政策
              本平台尊重并保护所有使用服务用户的个人隐私权。为了给您提供更准确、更有个性化的服务，本平台会按照本隐私权政策的规定使用和披露您的个人信息。但本平台将以高度的勤勉、审慎义务对待这些信息。除本隐私权政策另有规定外，在未征得您事先许可的情况下，本平台不会将这些信息对外披露或向第三方提供。本平台会不时更新本隐私权政策。
              您在同意本平台服务使用协议之时，即视为您已经同意本隐私权政策全部内容。本隐私权政策属于本平台服务使用协议不可分割的一部分。
              7.1.
              适用范围：在您注册本平台帐号时，您根据本平台要求提供的个人注册信息；在您使用本平台网络服务，或访问本平台平台网页时，本平台自动接收并记录的您的浏览器和计算机上的信息，包括但不限于您的IP地址、浏览器的类型、使用的语言、访问日期和时间、软硬件特征信息及您需求的网页记录等数据；在您使用本平台服务是上传的数据；
              7.2信息使用：本平台不会向任何无关第三方提供、出售、出租、分享或交易您的个人信息，除非事先得到您的许可；本平台亦不允许任何第三方以任何手段收集、编辑、出售或者无偿传播您的个人信息。任何本平台平台用户如从事上述活动，一经发现，本平台有权立即终止与该用户的服务协议；为服务用户的目的，本平台可能通过使用您上传的信息，进行模型的优化，向您提供更优质的服务。
              7.3在如下情况下，本平台将依据您的个人意愿或法律的规定全部或部分的披露您的个人信息：经您事先同意，向第三方披露；根据法律的有关规定，或者行政或司法机构的要求，向第三方或者行政、司法机构披露；如您出现违反中国有关法律、法规或者本平台服务协议或相关规则的情况，需要向第三方披露；如您是适格的知识产权投诉人并已提起投诉，应被投诉人要求，向被投诉人披露，以便双方处理可能的权利纠纷；在本平台平台上创建的某一交易中，如交易任何一方履行或部分履行了交易义务并提出信息披露请求的，本平台有权决定向该用户提供其交易对方的联络方式等必要信息，以促成交易的完成或纠纷的解决；其它本平台根据法律、法规或者网站政策认为合适的披露。
              7.4信息存储和交换：本平台收集的有关您的信息将保存在本平台及（或）其关联公司的服务器上，这些信息可能传送至您所在国家、地区或本平台收集信息和资料所在地的境外并在境外被访问、存储和展示。
              7.5在您未拒绝接受cookies的情况下，本平台会在您的计算机上设定或取用cookies
              ，以便您能登录或使用依赖于cookies的本平台平台服务或功能。本平台使用cookies可为您提供更加周到的个性化服务，包括推广服务；您有权选择接受或拒绝接受cookies。您可以通过修改浏览器设置的方式拒绝接受cookies。但如果您选择拒绝接受cookies，则您可能无法登录或使用依赖于cookies的本平台网络服务或功能；通过本平台所设cookies所取得的有关信息，将适用本政策。
              7.6本平台帐号均有安全保护功能，请妥善保管您的用户名及密码信息。本平台将通过对用户密码进行加密等安全措施确保您的信息不丢失，不被滥用和变造。尽管有前述安全措施，但同时也请您注意在信息网络上不存在“完善的安全措施”。
              8.其他约定
              8.1对不可抗力导致的损失本平台不承担责任。本协议所指不可抗力包括但不限于：天灾、法律法规或政府指令的变更，因网络服务特性而特有的原因，例如境内外基础电信运营商的故障、计算机或互联网相关技术缺陷、互联网覆盖范围限制、计算机病毒、黑客攻击等因素，及其他合法范围内的不能预见、不能避免并不能克服的客观情况。
              8.2可能会提供第三方国际互联网网站或资源链接，除非另有声明外，无法对第三方网站服务进行控制，因此由于下载、传播、使用或依赖上述网站或资源所产生的损失或损害，本不承担任何责任。
              8.3在适用法律允许的最大范围内，本公司不就因用户使用引起的，或在任何方面与本公司的产品和服务有关的任何意外的、非直接的、特殊的、或间接的损害或请求（包括但不限于因人身伤害、因隐私泄漏、因未能履行包括诚信或合理谨慎在内的任何责任、因过失和因任何其他金钱上的损失或其他损失而造成的损害赔偿）承担任何责任。在适用法律允许的最大范围内，本公司明确表示不提供任何其他类型的保证，不论是明示的或默示的，包括但不限于适销性、适用性、可靠性、准确性、完整性、无病毒以及无错误的任何默示保证和责任。除法律法规另有明确规定外，本公司对用户承担的全部责任，无论因何原因或何种行为方式，始终不超过用户因使用而支付给本公司的费用（如有）。在适用法律允许的最大范围内，本公司及其许可人不会向用户做出以下声明或担保：(A)
              用户对服务的使用会满足用户的需求；(B)
              用户对服务的使用会连续无中断、及时、安全或没有错误；（C）用户使用相关服务而获得的任何信息一律准确可靠；（D）作为相关服务的一部分，向用户提供的任何软件所发生的操作或功能瑕疵将获得修正。
              8.4服务中止、中断及终止：出于自身商业决策、执行行政/司法机关的命令、维护本服务的安全、维护其他用户的正常使用与数据安全、回应其他主体的侵权诉求等理由，或者根据自身的判断，认为您的行为涉嫌违反本协议内容或涉嫌违反法律法规的规定的，则有权变更、中止、中断或终止向您提供服务，且无须向您或任何第三方承担责任。
              8.5所有发给您的通知都可通过用户短信、站内信息、电话、电子邮件、常规的信件或在本平台或网易网站内显著位置公告的方式进行传送。将通过上述方法之一将消息传递给您，告知您协议的修改、服务变更、或其它重要事项。同时，本公司保留在本平台中投放商业性广告的权利以及利用用户登录的网易邮箱发布商业性广告的权利，包括但不限于在网站、APP登录页面及登录后任何页面内放置商业广告、向用户发送商业性广告短信、邮件在用户发出的电子邮件内附上商业性广告及／或广告链接、电话销售等形式，但用户有权选择拒绝接受此类广告等信息。本公司将按照法律规定履行广告及推广相关义务，用户应当自行判断该等信息的真实性和可靠性并为自己的判断行为负责。除法律法规明确规定外，用户因该等信息进行的购买或交易或因前述内容遭受的损害或损失，用户应自行承担，本公司不予承担责任。
              8.6所有权及知识产权：本平台上所有内容，包括但不限于文字、软件、声音、图片、录像、图表、网站架构、网站画面的安排、网页设计、为您提供的课程及其他资料均由本平台或其他权利人依法拥有其知识产权，包括但不限于著作权、商标权、专利权等。非经本平台或其他权利人书面同意，您不得擅自使用、修改、复制、录像、传播、改变、散布、发行或发表上述内容。如有违反，您同意承担由此给本平台或其他权利人造成的一切损失。
              8.7为保证产品、服务的安全性及产品功能的一致性，本公司可能会对软件进行更新。用户应将软件更新到最新版本，如用户未及时更新到最新版本，本公司不保证用户一定能正常使用服务。
              8.8本协议适用中华人民共和国的法律（不含冲突法）。
              当本协议的任何内容与中华人民共和国法律相抵触时，应当以法律规定为准，同时相关内容将按法律规定进行修改或重新解释，而本协议其他部分的法律效力不变。
              8.9凡因本协议引起的或与本协议有关的任何争议，均应提交中国国际经济贸易仲裁委员会，按照申请仲裁时该会现行有效的仲裁规则在中国北京进行仲裁，并由3名仲裁员进行审理。仲裁裁决是终局的，对双方均有约束力。
              8.10不行使、未能及时行使或者未充分行使本协议或者按照法律规定所享有的权利，不应被视为放弃该权利，也不影响在将来行使该权利。</span
            >
          </div>
          <span slot="footer" class="dialog-footer">
            <el-button type="primary" @click="dialogVisible = false"
              >确 定</el-button
            >
          </span>
        </el-dialog>
        <el-button
          type="primary"
          @click="mutilHandler"
          :disabled="isUploadTextDisable"
          >上传文件<i class="el-icon-upload el-icon--right"></i
        ></el-button>
        <div v-show="progressFlag" class="head-img">
          <el-progress
            :text-inside="true"
            :stroke-width="14"
            :percentage="progressPercent"
            status="success"
          ></el-progress>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// 引入子组件
import SubAdd from "./SubAdd";
export default {
  data() {
    return {
      comName: [],
      formData: new FormData(),
      fileList: [],
      num: 0,
      isAgree: false,
      dialogVisible: false,
      isUploadTextDisable: false,
      progressFlag: false,
      progressPercent: 0,
      loading: false,
    };
  },
  components: {
    SubAdd,
  },
  mounted() {
    this.zujian();
  },
  methods: {
    showDialog() {
      this.dialogVisible = true;
    },
    // 添加组件1
    zujian() {
      if (this.comName.length > 4) {
        this.$message.error("只能上传5个项目！");
        return;
      }
      ++this.num;
      console.log("this.num=>", this.num);
      this.comName.push({
        name: "SubAdd",
        id: this.num,
      });
    },
    // remove文件后删除组件
    removeFile(idx) {
      this.fileList.splice(idx, 1);
      console.log("removeFile=>", this.fileList.length);
    },
    // 删除组件
    getContent(index) {
      console.log("getContent=>", index);
      this.comName.splice(index, 1);
      this.fileList.splice(index, 1);

      console.log("getContentFileListLength=>", this.fileList.length);
    },
    // 从子组件保存文件
    saveFile(fileInfo) {
      console.log("从子组件保存文件");
      var file = fileInfo.file;
      console.log("saveFile.file=>", file);
      var idx = fileInfo.idx;
      var planName = fileInfo.planName;

      if (idx < this.fileList.length) {
        this.fileList[idx].file = file;
        this.fileList[idx].planName = planName;
      } else {
        this.fileList.push(fileInfo);
      }
      console.log("this.fileList.length=>", this.fileList.length);
      // let formData = new FormData();
      //   this.formData.append("fil", file);
      // formData.append("idx", idx);
      // console.log("idx=>", idx);
      // console.log("this.fileForm[idx]=>", this.fileForm[idx])
      // if (this.fileForm[idx] === undefined) {
      //     this.fileForm.push({'data': formData, 'index': idx});
      // }
      // else {
      //     this.fileForm[idx].data = formData;
      // }
      // console.log("fileForm.length=>", this.fileForm.length);
    },
    mutilHandler() {
      //   this.formData.append("fileList", this.fileList);
      if (this.fileList.length === 0) {
        this.$message.error("请至少上传一个文件！");
        return;
      }
      if (this.isAgree === false) {
        this.$message.error("请同意并接受左侧服务协议！");
        return;
      }
      for (var i = 0; i < this.fileList.length; i++) {
        this.formData.append("files", this.fileList[i].file);
        this.formData.append("planName", this.fileList[i].planName);
      }
      console.log("mutil=>", this.formData.getAll("files"));
      console.log("mutil=>", this.formData.getAll("planName"));

      this.isUploadTextDisable = true;
      var that = this;
      that.progressFlag = true;
      this.$axios
        .post("/handler", this.formData, {
          headers: { "Content-Type": "multipart/form-data" },
          onUploadProgress: (ProgressEvent) => {
            that.progressPercent =
              ((ProgressEvent.loaded / ProgressEvent.total) * 100) | 0;
            if (that.progressPercent >= 100) {
              that.$message.success("文件上传成功，请耐心等待解析...");
              that.loading = true;
            }
          },
        })
        .then((response) => {
          if (response) {
            if (response.data.code === 10000) {
              this.$message.success("导入成功");

              var dataStr = JSON.stringify(response.data);
              console.log("dataStr=>", dataStr);
              // console.log("dataStr[0]=>", dataStr[0]);
              sessionStorage.setItem("scoredata", dataStr);
              this.$router.push({
                name: "查看评分",
                params: { responses: response },
              });
            } else if (response.data.code === 11100) {
              this.$message.error("文件不合法，请重新上传！");
            } else if (response.data.code === 11111) {
              this.$message.error("抱谦，您上传的文档无法正确识别！");
            }
          }
          this.isUploadTextDisable = false;
          this.progressFlag = false;
          this.progressPercent = 0;
          this.loading = false;
          this.comName = [];
          this.fileList = [];
          // this.formData = new FormData();
        });
    },
  },
};
</script>
