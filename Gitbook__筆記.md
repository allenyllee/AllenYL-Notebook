# Gitbook__筆記

## plugins
- [aleen42/gitbook-treeview: A gitbook plugin for generating tree view for ech page](https://github.com/aleen42/gitbook-treeview)

## TroubleShooting

- [Windows only "Template render error expected variable end" · Issue #1827 · GitbookIO/gitbook](https://github.com/GitbookIO/gitbook/issues/1827)

    > If your code contains templating syntax such as \{\{ this \}\} (see templating), you can disable templating with a {% raw %}{% endraw %} block:+
    > 
    > For example:
    > 
    > {% raw %}
    > 
    > ```js
    > var Dialog = require('ysp-interior-components').Dialog;
    > module.exports = React.createClass({
    > 
    >   getInitialState: function() {
    >     return { open: false };
    >   },
    > 
    >   handleClick: function() {
    >       this.setState({
    >         open: !this.state.open
    >     });
    >   },
    > 
    >   render: function() {
    >       return (
    >       <div>
    >         <AMUI.Button onClick={this.handleClick}>点我显示弹窗</AMUI.Button>
    >         {this.state.open &&
    >           <Dialog config={{status: "real"}}>
    >             <h4 className="modal-title">Modal 标题</h4>
    >             <span onClick={this.handleClick} className="icon icon-close modal-icon"></span>
    >             <div className="modal-body">Hello, Modal 内容</div>
    >           </Dialog>}
    >       </div>
    >     );
    >   }
    > });
    > ```
    > 
    > {% endraw %}
